---
title: Azure Media Services - Smooth Streaming Protocol (MS-SSTR) Amendment for HEVC | Microsoft Docs
description: This specification describes the protocol and format for fragmented MP4-based live streaming with HEVC in Azure Media Services. This is an amendment to the Smooth Streaming protocol documentaiton (MS-SSTR) to include support for HEVC ingest and streaming. Only the changes required to deliver HEVC are specified in this article, except were “(No Change)” indicates text is copied for clarification only.
services: media-services
documentationcenter: ''
author: cenkdin
manager: cfowler
editor: ''
ms.assetid: f27d85de-2cb8-4269-8eed-2efb566ca2c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2018
ms.author: johndeu;
ms.openlocfilehash: 78ec0e3ee4304e820bf64afa26440380887630a1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969199"
---
# <a name="smooth-streaming-protocol-ms-sstr-amendment-for-hevc"></a><span data-ttu-id="503cc-105">Smooth Streaming Protocol (MS-SSTR) Amendment for HEVC</span><span class="sxs-lookup"><span data-stu-id="503cc-105">Smooth Streaming Protocol (MS-SSTR) Amendment for HEVC</span></span>

## <a name="1-introduction"></a><span data-ttu-id="503cc-106">1 Introduction</span><span class="sxs-lookup"><span data-stu-id="503cc-106">1 Introduction</span></span> 

<span data-ttu-id="503cc-107">This article provides detailed amendments to be applied to the Smooth Streaming Protocol specification [MS-SSTR] to enable Smooth Streaming of HEVC encoded video.</span><span class="sxs-lookup"><span data-stu-id="503cc-107">This article provides detailed amendments to be applied to the Smooth Streaming Protocol specification [MS-SSTR] to enable Smooth Streaming of HEVC encoded video.</span></span> <span data-ttu-id="503cc-108">In this specification, we outline only the changes required to deliver the HEVC video codec.</span><span class="sxs-lookup"><span data-stu-id="503cc-108">In this specification, we outline only the changes required to deliver the HEVC video codec.</span></span> <span data-ttu-id="503cc-109">The article follows the same numbering schema as the [MS-SSTR] specification.</span><span class="sxs-lookup"><span data-stu-id="503cc-109">The article follows the same numbering schema as the [MS-SSTR] specification.</span></span> <span data-ttu-id="503cc-110">The empty headlines presented throughout the article are provided to orient the reader to their position in the [MS-SSTR] specification.</span><span class="sxs-lookup"><span data-stu-id="503cc-110">The empty headlines presented throughout the article are provided to orient the reader to their position in the [MS-SSTR] specification.</span></span>  <span data-ttu-id="503cc-111">“(No Change)” indicates text is copied for clarification purposes only.</span><span class="sxs-lookup"><span data-stu-id="503cc-111">“(No Change)” indicates text is copied for clarification purposes only.</span></span>

<span data-ttu-id="503cc-112">The article provides technical implementation requirements for the signaling of HEVC video codec in a Smooth Streaming manifest and normative  references are updated to reference the current MPEG standards that include HEVC, Common Encryption of HEVC, and box names for ISO Base Media File Format have been updated to be consistent with the latest specifications.</span><span class="sxs-lookup"><span data-stu-id="503cc-112">The article provides technical implementation requirements for the signaling of HEVC video codec in a Smooth Streaming manifest and normative  references are updated to reference the current MPEG standards that include HEVC, Common Encryption of HEVC, and box names for ISO Base Media File Format have been updated to be consistent with the latest specifications.</span></span> 

<span data-ttu-id="503cc-113">The referenced Smooth Streaming Protocol specification [MS-SSTR] describes the wire format used to deliver live and on-demand digital media, such as audio and video, in the following manners: from an encoder to a web server, from a server to another server, and from a server to an HTTP client.</span><span class="sxs-lookup"><span data-stu-id="503cc-113">The referenced Smooth Streaming Protocol specification [MS-SSTR] describes the wire format used to deliver live and on-demand digital media, such as audio and video, in the following manners: from an encoder to a web server, from a server to another server, and from a server to an HTTP client.</span></span>
<span data-ttu-id="503cc-114">The use of an MPEG-4 ([[MPEG4-RA])](http://go.microsoft.com/fwlink/?LinkId=327787)-based data structure delivery over HTTP allows seamless switching in near real time between different quality levels of compressed media content.</span><span class="sxs-lookup"><span data-stu-id="503cc-114">The use of an MPEG-4 ([[MPEG4-RA])](http://go.microsoft.com/fwlink/?LinkId=327787)-based data structure delivery over HTTP allows seamless switching in near real time between different quality levels of compressed media content.</span></span> <span data-ttu-id="503cc-115">The result is a constant playback experience for the HTTP client end user, even if network and video rendering conditions change for the client computer or device.</span><span class="sxs-lookup"><span data-stu-id="503cc-115">The result is a constant playback experience for the HTTP client end user, even if network and video rendering conditions change for the client computer or device.</span></span>

## <a name="11-glossary"></a><span data-ttu-id="503cc-116">1.1 Glossary</span><span class="sxs-lookup"><span data-stu-id="503cc-116">1.1 Glossary</span></span> 

<span data-ttu-id="503cc-117">The following terms are defined in *[MS-GLOS]*:</span><span class="sxs-lookup"><span data-stu-id="503cc-117">The following terms are defined in *[MS-GLOS]*:</span></span>

>   <span data-ttu-id="503cc-118">**globally unique identifier (GUID) universally unique identifier (UUID)**</span><span class="sxs-lookup"><span data-stu-id="503cc-118">**globally unique identifier (GUID) universally unique identifier (UUID)**</span></span>

<span data-ttu-id="503cc-119">The following terms are specific to this document:</span><span class="sxs-lookup"><span data-stu-id="503cc-119">The following terms are specific to this document:</span></span>

>  <span data-ttu-id="503cc-120">**composition time:** The time a sample is presented at the client,   as defined in   [[ISO/IEC-14496-12].](http://go.microsoft.com/fwlink/?LinkId=183695)</span><span class="sxs-lookup"><span data-stu-id="503cc-120">**composition time:** The time a sample is presented at the client,   as defined in   [[ISO/IEC-14496-12].](http://go.microsoft.com/fwlink/?LinkId=183695)</span></span>

>   <span data-ttu-id="503cc-121">**CENC**: Common Encryption, as defined in [ISO/IEC 23001-7] Second Edition.</span><span class="sxs-lookup"><span data-stu-id="503cc-121">**CENC**: Common Encryption, as defined in [ISO/IEC 23001-7] Second Edition.</span></span>

>   <span data-ttu-id="503cc-122">**decode time:** The time a sample is required to be decoded on the client,   as defined in   [[ISO/IEChttp://go.microsoft.com/fwlink/?LinkId=18369514496-12].](http://go.microsoft.com/fwlink/?LinkId=183695)</span><span class="sxs-lookup"><span data-stu-id="503cc-122">**decode time:** The time a sample is required to be decoded on the client,   as defined in   [[ISO/IEChttp://go.microsoft.com/fwlink/?LinkId=18369514496-12].](http://go.microsoft.com/fwlink/?LinkId=183695)</span></span>

<span data-ttu-id="503cc-123">**fragment:** An independently downloadable unit of **media** that comprises one or more **samples**.</span><span class="sxs-lookup"><span data-stu-id="503cc-123">**fragment:** An independently downloadable unit of **media** that comprises one or more **samples**.</span></span>

>   <span data-ttu-id="503cc-124">**HEVC:** High Efficiency Video Coding, as defined in [ISO/IEC 23008-2]</span><span class="sxs-lookup"><span data-stu-id="503cc-124">**HEVC:** High Efficiency Video Coding, as defined in [ISO/IEC 23008-2]</span></span>

>   <span data-ttu-id="503cc-125">**manifest:** Metadata about the **presentation** that allows a client to make requests for **media**.</span><span class="sxs-lookup"><span data-stu-id="503cc-125">**manifest:** Metadata about the **presentation** that allows a client to make requests for **media**.</span></span> <span data-ttu-id="503cc-126">**media:** Compressed audio, video, and text data used by the client to play a **presentation**.</span><span class="sxs-lookup"><span data-stu-id="503cc-126">**media:** Compressed audio, video, and text data used by the client to play a **presentation**.</span></span> <span data-ttu-id="503cc-127">**media format:** A well-defined format for representing audio or video as a compressed **sample**.</span><span class="sxs-lookup"><span data-stu-id="503cc-127">**media format:** A well-defined format for representing audio or video as a compressed **sample**.</span></span>

>   <span data-ttu-id="503cc-128">**presentation:** The set of all **streams** and related metadata needed to play a single movie.</span><span class="sxs-lookup"><span data-stu-id="503cc-128">**presentation:** The set of all **streams** and related metadata needed to play a single movie.</span></span> <span data-ttu-id="503cc-129">**request:** An HTTP message sent from the client to the server, as defined in [[RFC2616].](http://go.microsoft.com/fwlink/?LinkId=90372)</span><span class="sxs-lookup"><span data-stu-id="503cc-129">**request:** An HTTP message sent from the client to the server, as defined in [[RFC2616].](http://go.microsoft.com/fwlink/?LinkId=90372)</span></span> <span data-ttu-id="503cc-130">**response:** An HTTP message sent from the server to the client, as defined in [[RFC2616].](http://go.microsoft.com/fwlink/?LinkId=90372)</span><span class="sxs-lookup"><span data-stu-id="503cc-130">**response:** An HTTP message sent from the server to the client, as defined in [[RFC2616].](http://go.microsoft.com/fwlink/?LinkId=90372)</span></span>

>   <span data-ttu-id="503cc-131">**sample:** The smallest fundamental unit (such as a frame) in which   **media** is stored and processed.</span><span class="sxs-lookup"><span data-stu-id="503cc-131">**sample:** The smallest fundamental unit (such as a frame) in which   **media** is stored and processed.</span></span>

>   <span data-ttu-id="503cc-132">**MAY, SHOULD, MUST, SHOULD NOT, MUST NOT:** These terms (in all caps) are used as described in [[RFC2119].](http://go.microsoft.com/fwlink/?LinkId=90317)</span><span class="sxs-lookup"><span data-stu-id="503cc-132">**MAY, SHOULD, MUST, SHOULD NOT, MUST NOT:** These terms (in all caps) are used as described in [[RFC2119].](http://go.microsoft.com/fwlink/?LinkId=90317)</span></span> <span data-ttu-id="503cc-133">All statements of optional behavior use either MAY, SHOULD, or SHOULD NOT.</span><span class="sxs-lookup"><span data-stu-id="503cc-133">All statements of optional behavior use either MAY, SHOULD, or SHOULD NOT.</span></span>

## <a name="12-references"></a><span data-ttu-id="503cc-134">1.2 References</span><span class="sxs-lookup"><span data-stu-id="503cc-134">1.2 References</span></span> 
-----------

>   <span data-ttu-id="503cc-135">References to Microsoft Open Specifications documentation do not include a publishing year because links are to the latest version of the documents, which are updated frequently.</span><span class="sxs-lookup"><span data-stu-id="503cc-135">References to Microsoft Open Specifications documentation do not include a publishing year because links are to the latest version of the documents, which are updated frequently.</span></span> <span data-ttu-id="503cc-136">References to other documents include a publishing year when one is available.</span><span class="sxs-lookup"><span data-stu-id="503cc-136">References to other documents include a publishing year when one is available.</span></span>

 ### <a name="121-normative-references"></a><span data-ttu-id="503cc-137">1.2.1 Normative References</span><span class="sxs-lookup"><span data-stu-id="503cc-137">1.2.1 Normative References</span></span> 

>  <span data-ttu-id="503cc-138">[MS-SSTR] Smooth Streaming Protocol *v20140502* [http://download.microsoft.com/download/9/5/E/95EF66AF-9026-4BB0-A41D-A4F81802D92C/[MS-SSTR].pdf](http://download.microsoft.com/download/9/5/E/95EF66AF-9026-4BB0-A41D-A4F81802D92C/%5bMS-SSTR%5d.pdf)</span><span class="sxs-lookup"><span data-stu-id="503cc-138">[MS-SSTR] Smooth Streaming Protocol *v20140502* [http://download.microsoft.com/download/9/5/E/95EF66AF-9026-4BB0-A41D-A4F81802D92C/[MS-SSTR].pdf](http://download.microsoft.com/download/9/5/E/95EF66AF-9026-4BB0-A41D-A4F81802D92C/%5bMS-SSTR%5d.pdf)</span></span>

>   <span data-ttu-id="503cc-139">[ISO/IEC 14496-12] International Organization for Standardization, "Information technology -- Coding of audio-visual objects -- Part 12: ISO Base Media File Format", ISO/IEC 14496-12:2014, Edition 4, Plus Corrigendum 1, Amendments 1 & 2.</span><span class="sxs-lookup"><span data-stu-id="503cc-139">[ISO/IEC 14496-12] International Organization for Standardization, "Information technology -- Coding of audio-visual objects -- Part 12: ISO Base Media File Format", ISO/IEC 14496-12:2014, Edition 4, Plus Corrigendum 1, Amendments 1 & 2.</span></span>
>   <http://standards.iso.org/ittf/PubliclyAvailableStandards/c061988_ISO_IEC_14496-12_2012.zip>

>   <span data-ttu-id="503cc-140">[ISO/IEC 14496-15] International Organization for Standardization, "Information technology -- Coding of audio-visual objects -- Part 15: Carriage of NAL unit structured video in the ISO Base Media File Format", ISO 14496-15:2015, Edition 3.</span><span class="sxs-lookup"><span data-stu-id="503cc-140">[ISO/IEC 14496-15] International Organization for Standardization, "Information technology -- Coding of audio-visual objects -- Part 15: Carriage of NAL unit structured video in the ISO Base Media File Format", ISO 14496-15:2015, Edition 3.</span></span>
>   <http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=65216>

>   <span data-ttu-id="503cc-141">[ISO/IEC 23008-2] Information technology -- High efficiency coding and media   delivery in heterogeneous environments -- Part 2: High efficiency video   coding: 2013 or newest edition   <http://standards.iso.org/ittf/PubliclyAvailableStandards/c035424_ISO_IEC_23008-2_2013.zip></span><span class="sxs-lookup"><span data-stu-id="503cc-141">[ISO/IEC 23008-2] Information technology -- High efficiency coding and media   delivery in heterogeneous environments -- Part 2: High efficiency video   coding: 2013 or newest edition   <http://standards.iso.org/ittf/PubliclyAvailableStandards/c035424_ISO_IEC_23008-2_2013.zip></span></span>

>   <span data-ttu-id="503cc-142">[ISO/IEC 23001-7] Information technology — MPEG systems technologies — Part   7: Common encryption in ISO base media file format files, CENC Edition   2:2015 <http://www.iso.org/iso/catalogue_detail.htm?csnumber=65271></span><span class="sxs-lookup"><span data-stu-id="503cc-142">[ISO/IEC 23001-7] Information technology — MPEG systems technologies — Part   7: Common encryption in ISO base media file format files, CENC Edition   2:2015 <http://www.iso.org/iso/catalogue_detail.htm?csnumber=65271></span></span>

>   <span data-ttu-id="503cc-143">[RFC-6381] IETF RFC-6381, “The 'Codecs' and 'Profiles' Parameters for   "Bucket" Media Types” <http://tools.ietf.org/html/rfc6381></span><span class="sxs-lookup"><span data-stu-id="503cc-143">[RFC-6381] IETF RFC-6381, “The 'Codecs' and 'Profiles' Parameters for   "Bucket" Media Types” <http://tools.ietf.org/html/rfc6381></span></span>

>   <span data-ttu-id="503cc-144">[MPEG4-RA] The MP4 Registration Authority, "MP4REG", [http://www.mp4ra.org   ](http://go.microsoft.com/fwlink/?LinkId=327787)</span><span class="sxs-lookup"><span data-stu-id="503cc-144">[MPEG4-RA] The MP4 Registration Authority, "MP4REG", [http://www.mp4ra.org   ](http://go.microsoft.com/fwlink/?LinkId=327787)</span></span>

>   <span data-ttu-id="503cc-145">[RFC2119] Bradner, S., "Key words for use in RFCs to Indicate Requirement   Levels", BCP 14, RFC 2119, March 1997,   [http://www.rfc-editor.org/rfc/rfc2119.txt   ](http://go.microsoft.com/fwlink/?LinkId=90317)</span><span class="sxs-lookup"><span data-stu-id="503cc-145">[RFC2119] Bradner, S., "Key words for use in RFCs to Indicate Requirement   Levels", BCP 14, RFC 2119, March 1997,   [http://www.rfc-editor.org/rfc/rfc2119.txt   ](http://go.microsoft.com/fwlink/?LinkId=90317)</span></span>

### <a name="122-informative-references"></a><span data-ttu-id="503cc-146">1.2.2 Informative References</span><span class="sxs-lookup"><span data-stu-id="503cc-146">1.2.2 Informative References</span></span> 

>   <span data-ttu-id="503cc-147">[MS-GLOS] Microsoft Corporation, "*Windows Protocols Master Glossary*."</span><span class="sxs-lookup"><span data-stu-id="503cc-147">[MS-GLOS] Microsoft Corporation, "*Windows Protocols Master Glossary*."</span></span>

>   <span data-ttu-id="503cc-148">[RFC3548] Josefsson, S., Ed., "The Base16, Base32, and Base64 Data   Encodings", RFC 3548, July 2003, [http://www.ietf.org/rfc/rfc3548.txt   ](http://go.microsoft.com/fwlink/?LinkId=90432)</span><span class="sxs-lookup"><span data-stu-id="503cc-148">[RFC3548] Josefsson, S., Ed., "The Base16, Base32, and Base64 Data   Encodings", RFC 3548, July 2003, [http://www.ietf.org/rfc/rfc3548.txt   ](http://go.microsoft.com/fwlink/?LinkId=90432)</span></span>

>   <span data-ttu-id="503cc-149">[RFC5234] Crocker, D., Ed., and Overell, P., "Augmented BNF for Syntax   Specifications: ABNF", STD 68, RFC 5234, January 2008,   [http://www.rfc-editor.org/rfc/rfc5234.txt   ](http://go.microsoft.com/fwlink/?LinkId=123096)</span><span class="sxs-lookup"><span data-stu-id="503cc-149">[RFC5234] Crocker, D., Ed., and Overell, P., "Augmented BNF for Syntax   Specifications: ABNF", STD 68, RFC 5234, January 2008,   [http://www.rfc-editor.org/rfc/rfc5234.txt   ](http://go.microsoft.com/fwlink/?LinkId=123096)</span></span>


## <a name="13-overview"></a><span data-ttu-id="503cc-150">1.3 Overview</span><span class="sxs-lookup"><span data-stu-id="503cc-150">1.3 Overview</span></span> 
---------

>   <span data-ttu-id="503cc-151">Only changes to the Smooth Streaming specification required for the delivery of HEVC are specified below.</span><span class="sxs-lookup"><span data-stu-id="503cc-151">Only changes to the Smooth Streaming specification required for the delivery of HEVC are specified below.</span></span> <span data-ttu-id="503cc-152">Unchanged section headers are listed to maintain location in the referenced Smooth Streaming specification [MS-SSTR].</span><span class="sxs-lookup"><span data-stu-id="503cc-152">Unchanged section headers are listed to maintain location in the referenced Smooth Streaming specification [MS-SSTR].</span></span>

## <a name="14-relationship-to-other-protocols"></a><span data-ttu-id="503cc-153">1.4 Relationship to Other Protocols</span><span class="sxs-lookup"><span data-stu-id="503cc-153">1.4 Relationship to Other Protocols</span></span> 
--------------------------------

## <a name="15-prerequisitespreconditions"></a><span data-ttu-id="503cc-154">1.5 Prerequisites/Preconditions</span><span class="sxs-lookup"><span data-stu-id="503cc-154">1.5 Prerequisites/Preconditions</span></span> 
----------------------------

## <a name="16-applicability-statement"></a><span data-ttu-id="503cc-155">1.6 Applicability Statement</span><span class="sxs-lookup"><span data-stu-id="503cc-155">1.6 Applicability Statement</span></span> 
------------------------

## <a name="17-versioning-and-capability-negotiation"></a><span data-ttu-id="503cc-156">1.7 Versioning and Capability Negotiation</span><span class="sxs-lookup"><span data-stu-id="503cc-156">1.7 Versioning and Capability Negotiation</span></span> 
--------------------------------------

## <a name="18-vendor-extensible-fields"></a><span data-ttu-id="503cc-157">1.8 Vendor-Extensible Fields</span><span class="sxs-lookup"><span data-stu-id="503cc-157">1.8 Vendor-Extensible Fields</span></span> 
-------------------------

>   <span data-ttu-id="503cc-158">The following method SHALL be used identify streams using the HEVC video   format:</span><span class="sxs-lookup"><span data-stu-id="503cc-158">The following method SHALL be used identify streams using the HEVC video   format:</span></span>

>   * <span data-ttu-id="503cc-159">**Custom Descriptive Codes for Media Formats:** This capability is provided by the **FourCC** field, as specified in section *2.2.2.5*.</span><span class="sxs-lookup"><span data-stu-id="503cc-159">**Custom Descriptive Codes for Media Formats:** This capability is provided by the **FourCC** field, as specified in section *2.2.2.5*.</span></span>
>   <span data-ttu-id="503cc-160">Implementers can ensure that extensions do not conflict by registering extension codes with the MPEG4-RA, as specified in [[ISO/IEC-14496-12] ](http://go.microsoft.com/fwlink/?LinkId=183695)</span><span class="sxs-lookup"><span data-stu-id="503cc-160">Implementers can ensure that extensions do not conflict by registering extension codes with the MPEG4-RA, as specified in [[ISO/IEC-14496-12] ](http://go.microsoft.com/fwlink/?LinkId=183695)</span></span>

## <a name="19-standards-assignments"></a><span data-ttu-id="503cc-161">1.9 Standards Assignments</span><span class="sxs-lookup"><span data-stu-id="503cc-161">1.9 Standards Assignments</span></span> 
----------------------

# <a name="2-messages"></a><span data-ttu-id="503cc-162">2 Messages</span><span class="sxs-lookup"><span data-stu-id="503cc-162">2 Messages</span></span> 

## <a name="21-transport"></a><span data-ttu-id="503cc-163">2.1 Transport</span><span class="sxs-lookup"><span data-stu-id="503cc-163">2.1 Transport</span></span> 
----------

## <a name="22-message-syntax"></a><span data-ttu-id="503cc-164">2.2 Message Syntax</span><span class="sxs-lookup"><span data-stu-id="503cc-164">2.2 Message Syntax</span></span> 
---------------

### <a name="221-manifest-request"></a><span data-ttu-id="503cc-165">2.2.1 Manifest Request</span><span class="sxs-lookup"><span data-stu-id="503cc-165">2.2.1 Manifest Request</span></span> 

### <a name="222-manifest-response"></a><span data-ttu-id="503cc-166">2.2.2 Manifest Response</span><span class="sxs-lookup"><span data-stu-id="503cc-166">2.2.2 Manifest Response</span></span> 

#### <a name="2221-smoothstreamingmedia"></a><span data-ttu-id="503cc-167">2.2.2.1 SmoothStreamingMedia</span><span class="sxs-lookup"><span data-stu-id="503cc-167">2.2.2.1 SmoothStreamingMedia</span></span> 

>   <span data-ttu-id="503cc-168">**MinorVersion (variable):** The minor version of the Manifest Response message.</span><span class="sxs-lookup"><span data-stu-id="503cc-168">**MinorVersion (variable):** The minor version of the Manifest Response message.</span></span> <span data-ttu-id="503cc-169">MUST be set to 2.</span><span class="sxs-lookup"><span data-stu-id="503cc-169">MUST be set to 2.</span></span> <span data-ttu-id="503cc-170">(No Change)</span><span class="sxs-lookup"><span data-stu-id="503cc-170">(No Change)</span></span>

>   <span data-ttu-id="503cc-171">**TimeScale (variable):** The time scale of the Duration attribute, specified as the number of increments in one second.</span><span class="sxs-lookup"><span data-stu-id="503cc-171">**TimeScale (variable):** The time scale of the Duration attribute, specified as the number of increments in one second.</span></span> <span data-ttu-id="503cc-172">The default value is</span><span class="sxs-lookup"><span data-stu-id="503cc-172">The default value is</span></span>
>   10000000. <span data-ttu-id="503cc-173">(No Change)</span><span class="sxs-lookup"><span data-stu-id="503cc-173">(No Change)</span></span>

>   <span data-ttu-id="503cc-174">The recommended value is 90000 for representing the exact duration of video   frames and fragments containing fractional framerate video (for example, 30/1.001   Hz).</span><span class="sxs-lookup"><span data-stu-id="503cc-174">The recommended value is 90000 for representing the exact duration of video   frames and fragments containing fractional framerate video (for example, 30/1.001   Hz).</span></span>

#### <a name="2222-protectionelement"></a><span data-ttu-id="503cc-175">2.2.2.2 ProtectionElement</span><span class="sxs-lookup"><span data-stu-id="503cc-175">2.2.2.2 ProtectionElement</span></span> 

<span data-ttu-id="503cc-176">The ProtectionElement SHALL be present when Common Encryption (CENC) has been applied to video or audio streams.</span><span class="sxs-lookup"><span data-stu-id="503cc-176">The ProtectionElement SHALL be present when Common Encryption (CENC) has been applied to video or audio streams.</span></span> <span data-ttu-id="503cc-177">HEVC encrypted streams SHALL conform to Common Encryption 2nd Edition [ISO/IEC 23001-7].</span><span class="sxs-lookup"><span data-stu-id="503cc-177">HEVC encrypted streams SHALL conform to Common Encryption 2nd Edition [ISO/IEC 23001-7].</span></span> <span data-ttu-id="503cc-178">Only slice data in VCL NAL Units SHALL be encrypted.</span><span class="sxs-lookup"><span data-stu-id="503cc-178">Only slice data in VCL NAL Units SHALL be encrypted.</span></span>

#### <a name="2223-streamelement"></a><span data-ttu-id="503cc-179">2.2.2.3 StreamElement</span><span class="sxs-lookup"><span data-stu-id="503cc-179">2.2.2.3 StreamElement</span></span> 

>   <span data-ttu-id="503cc-180">**StreamTimeScale (variable):** The time scale for duration and time values in this stream, specified as the number of increments in one second.</span><span class="sxs-lookup"><span data-stu-id="503cc-180">**StreamTimeScale (variable):** The time scale for duration and time values in this stream, specified as the number of increments in one second.</span></span> <span data-ttu-id="503cc-181">A value of 90000 is recommended for HEVC streams.</span><span class="sxs-lookup"><span data-stu-id="503cc-181">A value of 90000 is recommended for HEVC streams.</span></span> <span data-ttu-id="503cc-182">A value matching the waveform sample frequency (for example, 48000 or 44100) is recommended for audio streams.</span><span class="sxs-lookup"><span data-stu-id="503cc-182">A value matching the waveform sample frequency (for example, 48000 or 44100) is recommended for audio streams.</span></span>

##### <a name="22231-streamprotectionelement"></a><span data-ttu-id="503cc-183">2.2.2.3.1 StreamProtectionElement</span><span class="sxs-lookup"><span data-stu-id="503cc-183">2.2.2.3.1 StreamProtectionElement</span></span>

#### <a name="2224-urlpattern"></a><span data-ttu-id="503cc-184">2.2.2.4 UrlPattern</span><span class="sxs-lookup"><span data-stu-id="503cc-184">2.2.2.4 UrlPattern</span></span> 

#### <a name="225-trackelement"></a><span data-ttu-id="503cc-185">2.2.5 TrackElement</span><span class="sxs-lookup"><span data-stu-id="503cc-185">2.2.5 TrackElement</span></span> 

>   <span data-ttu-id="503cc-186">**FourCC (variable):** A four-character code that identifies which media format is used for each sample.</span><span class="sxs-lookup"><span data-stu-id="503cc-186">**FourCC (variable):** A four-character code that identifies which media format is used for each sample.</span></span> <span data-ttu-id="503cc-187">The following range of values is reserved with the following semantic meanings:</span><span class="sxs-lookup"><span data-stu-id="503cc-187">The following range of values is reserved with the following semantic meanings:</span></span>

>  * <span data-ttu-id="503cc-188">"hev1”: Video samples for this track use HEVC video, using the ‘hev1’ sample description format specified in [ISO/IEC-14496-15].</span><span class="sxs-lookup"><span data-stu-id="503cc-188">"hev1”: Video samples for this track use HEVC video, using the ‘hev1’ sample description format specified in [ISO/IEC-14496-15].</span></span>

>   <span data-ttu-id="503cc-189">**CodecPrivateData (variable):** Data that specifies parameters specific to the media format and common to all samples in the track, represented as a string of hex-coded bytes.</span><span class="sxs-lookup"><span data-stu-id="503cc-189">**CodecPrivateData (variable):** Data that specifies parameters specific to the media format and common to all samples in the track, represented as a string of hex-coded bytes.</span></span> <span data-ttu-id="503cc-190">The format and semantic meaning of byte sequence varies with the value of the **FourCC** field as follows:</span><span class="sxs-lookup"><span data-stu-id="503cc-190">The format and semantic meaning of byte sequence varies with the value of the **FourCC** field as follows:</span></span>

>   * <span data-ttu-id="503cc-191">When a TrackElement describes HEVC video, the **FourCC** field SHALL equal **"hev1"** and;</span><span class="sxs-lookup"><span data-stu-id="503cc-191">When a TrackElement describes HEVC video, the **FourCC** field SHALL equal **"hev1"** and;</span></span>

>   <span data-ttu-id="503cc-192">The **CodecPrivateData** field SHALL contain a hex-coded string   representation of the following byte sequence, specified in ABNF   [[RFC5234]:](http://go.microsoft.com/fwlink/?LinkId=123096) (no change from   MS-SSTR)</span><span class="sxs-lookup"><span data-stu-id="503cc-192">The **CodecPrivateData** field SHALL contain a hex-coded string   representation of the following byte sequence, specified in ABNF   [[RFC5234]:](http://go.microsoft.com/fwlink/?LinkId=123096) (no change from   MS-SSTR)</span></span>

>   * <span data-ttu-id="503cc-193">%x00 %x00 %x00 %x01 SPSField %x00 %x00 %x00 %x01 PPSField</span><span class="sxs-lookup"><span data-stu-id="503cc-193">%x00 %x00 %x00 %x01 SPSField %x00 %x00 %x00 %x01 PPSField</span></span>

>   * <span data-ttu-id="503cc-194">SPSField contains the Sequence Parameter Set (SPS).</span><span class="sxs-lookup"><span data-stu-id="503cc-194">SPSField contains the Sequence Parameter Set (SPS).</span></span>

>   * <span data-ttu-id="503cc-195">PPSField contains the Slice Parameter Set (PPS).</span><span class="sxs-lookup"><span data-stu-id="503cc-195">PPSField contains the Slice Parameter Set (PPS).</span></span>

>   <span data-ttu-id="503cc-196">Note: The Video Parameter Set (VPS) is not contained in CodecPrivateData, but should be contained in the file header of stored files in the ‘hvcC’ box.</span><span class="sxs-lookup"><span data-stu-id="503cc-196">Note: The Video Parameter Set (VPS) is not contained in CodecPrivateData, but should be contained in the file header of stored files in the ‘hvcC’ box.</span></span> <span data-ttu-id="503cc-197">Systems using Smooth Streaming Protocol must signal additional decoding parameters (for example, HEVC Tier) using the Custom Attribute “codecs.”</span><span class="sxs-lookup"><span data-stu-id="503cc-197">Systems using Smooth Streaming Protocol must signal additional decoding parameters (for example, HEVC Tier) using the Custom Attribute “codecs.”</span></span>

##### <a name="22251-customattributeselement"></a><span data-ttu-id="503cc-198">2.2.2.5.1 CustomAttributesElement</span><span class="sxs-lookup"><span data-stu-id="503cc-198">2.2.2.5.1 CustomAttributesElement</span></span> 

#### <a name="226-streamfragmentelement"></a><span data-ttu-id="503cc-199">2.2.6 StreamFragmentElement</span><span class="sxs-lookup"><span data-stu-id="503cc-199">2.2.6 StreamFragmentElement</span></span> 

>   <span data-ttu-id="503cc-200">The **SmoothStreamingMedia’s MajorVersion** field MUST be set to 2, and **MinorVersion** field MUST be set to 2.</span><span class="sxs-lookup"><span data-stu-id="503cc-200">The **SmoothStreamingMedia’s MajorVersion** field MUST be set to 2, and **MinorVersion** field MUST be set to 2.</span></span> <span data-ttu-id="503cc-201">(No Change)</span><span class="sxs-lookup"><span data-stu-id="503cc-201">(No Change)</span></span>

##### <a name="22261-trackfragmentelement"></a><span data-ttu-id="503cc-202">2.2.2.6.1 TrackFragmentElement</span><span class="sxs-lookup"><span data-stu-id="503cc-202">2.2.2.6.1 TrackFragmentElement</span></span> 

### <a name="223-fragment-request"></a><span data-ttu-id="503cc-203">2.2.3 Fragment Request</span><span class="sxs-lookup"><span data-stu-id="503cc-203">2.2.3 Fragment Request</span></span> 

>   <span data-ttu-id="503cc-204">**Note**: The default media format requested for **MinorVersion** 2 and ‘hev1’   is ‘iso8’ brand ISO Base Media File Format specified in [ISO/IEC 14496-12]   ISO Base Media File Format Fourth Edition, and [ISO/IEC 23001-7] Common   Encryption Second Edition.</span><span class="sxs-lookup"><span data-stu-id="503cc-204">**Note**: The default media format requested for **MinorVersion** 2 and ‘hev1’   is ‘iso8’ brand ISO Base Media File Format specified in [ISO/IEC 14496-12]   ISO Base Media File Format Fourth Edition, and [ISO/IEC 23001-7] Common   Encryption Second Edition.</span></span>

### <a name="224-fragment-response"></a><span data-ttu-id="503cc-205">2.2.4 Fragment Response</span><span class="sxs-lookup"><span data-stu-id="503cc-205">2.2.4 Fragment Response</span></span> 

#### <a name="2241-moofbox"></a><span data-ttu-id="503cc-206">2.2.4.1 MoofBox</span><span class="sxs-lookup"><span data-stu-id="503cc-206">2.2.4.1 MoofBox</span></span> 

#### <a name="2242-mfhdbox"></a><span data-ttu-id="503cc-207">2.2.4.2 MfhdBox</span><span class="sxs-lookup"><span data-stu-id="503cc-207">2.2.4.2 MfhdBox</span></span> 

#### <a name="2243-trafbox"></a><span data-ttu-id="503cc-208">2.2.4.3 TrafBox</span><span class="sxs-lookup"><span data-stu-id="503cc-208">2.2.4.3 TrafBox</span></span> 

#### <a name="2244-tfxdbox"></a><span data-ttu-id="503cc-209">2.2.4.4 TfxdBox</span><span class="sxs-lookup"><span data-stu-id="503cc-209">2.2.4.4 TfxdBox</span></span> 

>   <span data-ttu-id="503cc-210">The **TfxdBox** is deprecated, and its function replaced by the Track   Fragment Decode Time Box (‘tfdt’) specified in [ISO/IEC 14496-12] section   8.8.12.</span><span class="sxs-lookup"><span data-stu-id="503cc-210">The **TfxdBox** is deprecated, and its function replaced by the Track   Fragment Decode Time Box (‘tfdt’) specified in [ISO/IEC 14496-12] section   8.8.12.</span></span>

>   <span data-ttu-id="503cc-211">**Note**: A client may calculate the duration of a fragment by summing the sample durations listed in the Track Run Box (‘trun’) or multiplying the number of samples times the default sample duration.</span><span class="sxs-lookup"><span data-stu-id="503cc-211">**Note**: A client may calculate the duration of a fragment by summing the sample durations listed in the Track Run Box (‘trun’) or multiplying the number of samples times the default sample duration.</span></span> <span data-ttu-id="503cc-212">The baseMediaDecodeTime in ‘tfdt’ plus fragment duration equals the URL time parameter for the next fragment.</span><span class="sxs-lookup"><span data-stu-id="503cc-212">The baseMediaDecodeTime in ‘tfdt’ plus fragment duration equals the URL time parameter for the next fragment.</span></span>

>   <span data-ttu-id="503cc-213">A Producer Reference Time Box (‘prft’) SHOULD be inserted prior to a Movie   Fragment Box (‘moof’) as needed, to indicate the UTC time corresponding to   the Track Fragment Decode Time of the first sample referenced by the Movie   Fragment Box, as specified in [ISO/IEC 14496-12] section 8.16.5.</span><span class="sxs-lookup"><span data-stu-id="503cc-213">A Producer Reference Time Box (‘prft’) SHOULD be inserted prior to a Movie   Fragment Box (‘moof’) as needed, to indicate the UTC time corresponding to   the Track Fragment Decode Time of the first sample referenced by the Movie   Fragment Box, as specified in [ISO/IEC 14496-12] section 8.16.5.</span></span>

#### <a name="2245-tfrfbox"></a><span data-ttu-id="503cc-214">2.2.4.5 TfrfBox</span><span class="sxs-lookup"><span data-stu-id="503cc-214">2.2.4.5 TfrfBox</span></span> 

>   <span data-ttu-id="503cc-215">The **TfrfBox** is deprecated, and its function replaced by the Track   Fragment Decode Time Box (‘tfdt’) specified in [ISO/IEC 14496-12] section   8.8.12.</span><span class="sxs-lookup"><span data-stu-id="503cc-215">The **TfrfBox** is deprecated, and its function replaced by the Track   Fragment Decode Time Box (‘tfdt’) specified in [ISO/IEC 14496-12] section   8.8.12.</span></span>

>   <span data-ttu-id="503cc-216">**Note**: A client may calculate the duration of a fragment by summing the sample durations listed in the Track Run Box (‘trun’) or multiplying the number of samples times the default sample duration.</span><span class="sxs-lookup"><span data-stu-id="503cc-216">**Note**: A client may calculate the duration of a fragment by summing the sample durations listed in the Track Run Box (‘trun’) or multiplying the number of samples times the default sample duration.</span></span> <span data-ttu-id="503cc-217">The baseMediaDecodeTime in ‘tfdt’ plus fragment duration equals the URL time parameter for the next fragment.</span><span class="sxs-lookup"><span data-stu-id="503cc-217">The baseMediaDecodeTime in ‘tfdt’ plus fragment duration equals the URL time parameter for the next fragment.</span></span> <span data-ttu-id="503cc-218">Look ahead addresses are deprecated because they delay live streaming.</span><span class="sxs-lookup"><span data-stu-id="503cc-218">Look ahead addresses are deprecated because they delay live streaming.</span></span>

#### <a name="2246-tfhdbox"></a><span data-ttu-id="503cc-219">2.2.4.6 TfhdBox</span><span class="sxs-lookup"><span data-stu-id="503cc-219">2.2.4.6 TfhdBox</span></span> 

>   <span data-ttu-id="503cc-220">The **TfhdBox** and related fields encapsulate defaults for per sample metadata in the fragment.</span><span class="sxs-lookup"><span data-stu-id="503cc-220">The **TfhdBox** and related fields encapsulate defaults for per sample metadata in the fragment.</span></span> <span data-ttu-id="503cc-221">The syntax of the **TfhdBox** field is a strict subset of the syntax of the Track Fragment Header Box defined in [[ISO/IEC-14496-12]](http://go.microsoft.com/fwlink/?LinkId=183695) section 8.8.7.</span><span class="sxs-lookup"><span data-stu-id="503cc-221">The syntax of the **TfhdBox** field is a strict subset of the syntax of the Track Fragment Header Box defined in [[ISO/IEC-14496-12]](http://go.microsoft.com/fwlink/?LinkId=183695) section 8.8.7.</span></span>

>   <span data-ttu-id="503cc-222">**BaseDataOffset (8 bytes):** The offset, in bytes, from the beginning of the **MdatBox** field to the sample field in the **MdatBox** field.</span><span class="sxs-lookup"><span data-stu-id="503cc-222">**BaseDataOffset (8 bytes):** The offset, in bytes, from the beginning of the **MdatBox** field to the sample field in the **MdatBox** field.</span></span> <span data-ttu-id="503cc-223">To signal this restriction, the default-base-is-moof flag (0x020000) must be set.</span><span class="sxs-lookup"><span data-stu-id="503cc-223">To signal this restriction, the default-base-is-moof flag (0x020000) must be set.</span></span>

#### <a name="2247-trunbox"></a><span data-ttu-id="503cc-224">2.2.4.7 TrunBox</span><span class="sxs-lookup"><span data-stu-id="503cc-224">2.2.4.7 TrunBox</span></span> 

>   <span data-ttu-id="503cc-225">The **TrunBox** and related fields encapsulate per sample metadata for the requested fragment.</span><span class="sxs-lookup"><span data-stu-id="503cc-225">The **TrunBox** and related fields encapsulate per sample metadata for the requested fragment.</span></span> <span data-ttu-id="503cc-226">The syntax of **TrunBox** is a strict subset of the Version 1 Track Fragment Run Box defined in [[ISO/IEC-14496-](http://go.microsoft.com/fwlink/?LinkId=183695)*12]* section 8.8.8.</span><span class="sxs-lookup"><span data-stu-id="503cc-226">The syntax of **TrunBox** is a strict subset of the Version 1 Track Fragment Run Box defined in [[ISO/IEC-14496-](http://go.microsoft.com/fwlink/?LinkId=183695)*12]* section 8.8.8.</span></span>

>   <span data-ttu-id="503cc-227">**SampleCompositionTimeOffset (4 bytes):** The Sample Composition Time offset of each sample adjusted so that the presentation time of the first presented sample in the fragment is equal to the decode time of the first decoded sample.</span><span class="sxs-lookup"><span data-stu-id="503cc-227">**SampleCompositionTimeOffset (4 bytes):** The Sample Composition Time offset of each sample adjusted so that the presentation time of the first presented sample in the fragment is equal to the decode time of the first decoded sample.</span></span> <span data-ttu-id="503cc-228">Negative video sample composition offsets SHALL be used,</span><span class="sxs-lookup"><span data-stu-id="503cc-228">Negative video sample composition offsets SHALL be used,</span></span>

>   <span data-ttu-id="503cc-229">as defined in   [[ISO/IEC-14496-12].](http://go.microsoft.com/fwlink/?LinkId=183695)</span><span class="sxs-lookup"><span data-stu-id="503cc-229">as defined in   [[ISO/IEC-14496-12].](http://go.microsoft.com/fwlink/?LinkId=183695)</span></span>

>   <span data-ttu-id="503cc-230">Note: This avoids a video synchronization error caused by video lagging   audio equal to the largest decoded picture buffer removal delay, and   maintains presentation timing between alternative fragments that may have   different removal delays.</span><span class="sxs-lookup"><span data-stu-id="503cc-230">Note: This avoids a video synchronization error caused by video lagging   audio equal to the largest decoded picture buffer removal delay, and   maintains presentation timing between alternative fragments that may have   different removal delays.</span></span>

>   <span data-ttu-id="503cc-231">The syntax of the fields defined in this section, specified in ABNF   [[RFC5234],](http://go.microsoft.com/fwlink/?LinkId=123096) remains the   same, except as follows:</span><span class="sxs-lookup"><span data-stu-id="503cc-231">The syntax of the fields defined in this section, specified in ABNF   [[RFC5234],](http://go.microsoft.com/fwlink/?LinkId=123096) remains the   same, except as follows:</span></span>

>   <span data-ttu-id="503cc-232">SampleCompositionTimeOffset = SIGNED_INT32</span><span class="sxs-lookup"><span data-stu-id="503cc-232">SampleCompositionTimeOffset = SIGNED_INT32</span></span>

#### <a name="2248-mdatbox"></a><span data-ttu-id="503cc-233">2.2.4.8 MdatBox</span><span class="sxs-lookup"><span data-stu-id="503cc-233">2.2.4.8 MdatBox</span></span> 

#### <a name="2249-fragment-response-common-fields"></a><span data-ttu-id="503cc-234">2.2.4.9 Fragment Response Common Fields</span><span class="sxs-lookup"><span data-stu-id="503cc-234">2.2.4.9 Fragment Response Common Fields</span></span> 

### <a name="225-sparse-stream-pointer"></a><span data-ttu-id="503cc-235">2.2.5 Sparse Stream Pointer</span><span class="sxs-lookup"><span data-stu-id="503cc-235">2.2.5 Sparse Stream Pointer</span></span> 

### <a name="226-fragment-not-yet-available"></a><span data-ttu-id="503cc-236">2.2.6 Fragment Not Yet Available</span><span class="sxs-lookup"><span data-stu-id="503cc-236">2.2.6 Fragment Not Yet Available</span></span> 

### <a name="227-live-ingest"></a><span data-ttu-id="503cc-237">2.2.7 Live Ingest</span><span class="sxs-lookup"><span data-stu-id="503cc-237">2.2.7 Live Ingest</span></span> 

#### <a name="2271-filetype"></a><span data-ttu-id="503cc-238">2.2.7.1 FileType</span><span class="sxs-lookup"><span data-stu-id="503cc-238">2.2.7.1 FileType</span></span> 

>   <span data-ttu-id="503cc-239">**FileType (variable):** specifies the subtype and intended use of the   MPEG-4 ([[MPEG4-RA])](http://go.microsoft.com/fwlink/?LinkId=327787) file,   and high-level attributes.</span><span class="sxs-lookup"><span data-stu-id="503cc-239">**FileType (variable):** specifies the subtype and intended use of the   MPEG-4 ([[MPEG4-RA])](http://go.microsoft.com/fwlink/?LinkId=327787) file,   and high-level attributes.</span></span>

>   <span data-ttu-id="503cc-240">**MajorBrand (variable):** The major brand of the media file.</span><span class="sxs-lookup"><span data-stu-id="503cc-240">**MajorBrand (variable):** The major brand of the media file.</span></span> <span data-ttu-id="503cc-241">MUST be set to "isml."</span><span class="sxs-lookup"><span data-stu-id="503cc-241">MUST be set to "isml."</span></span>

>   <span data-ttu-id="503cc-242">**MinorVersion (variable):** The minor version of the media file.</span><span class="sxs-lookup"><span data-stu-id="503cc-242">**MinorVersion (variable):** The minor version of the media file.</span></span> <span data-ttu-id="503cc-243">MUST be set to 1.</span><span class="sxs-lookup"><span data-stu-id="503cc-243">MUST be set to 1.</span></span>

>   <span data-ttu-id="503cc-244">**CompatibleBrands (variable):** Specifies the supported brands of MPEG-4.</span><span class="sxs-lookup"><span data-stu-id="503cc-244">**CompatibleBrands (variable):** Specifies the supported brands of MPEG-4.</span></span>
>   <span data-ttu-id="503cc-245">MUST include "ccff" and "iso8."</span><span class="sxs-lookup"><span data-stu-id="503cc-245">MUST include "ccff" and "iso8."</span></span>

>   <span data-ttu-id="503cc-246">The syntax of the fields defined in this section, specified in ABNF   [[RFC5234],](http://go.microsoft.com/fwlink/?LinkId=123096) is as follows:</span><span class="sxs-lookup"><span data-stu-id="503cc-246">The syntax of the fields defined in this section, specified in ABNF   [[RFC5234],](http://go.microsoft.com/fwlink/?LinkId=123096) is as follows:</span></span>

    FileType = MajorBrand MinorVersion CompatibleBrands
    MajorBrand = STRING_UINT32
    MinorVersion = STRING_UINT32
    CompatibleBrands = "ccff" "iso8" 0\*(STRING_UINT32)

<span data-ttu-id="503cc-247">**Note**: The compatibility brands ‘ccff’ and ‘iso8’ indicate that fragments conform to “Common Container File Format” and Common Encryption [ISO/IEC 23001-7] and ISO Base Media File Format Edition 4 [ISO/IEC 14496-12].</span><span class="sxs-lookup"><span data-stu-id="503cc-247">**Note**: The compatibility brands ‘ccff’ and ‘iso8’ indicate that fragments conform to “Common Container File Format” and Common Encryption [ISO/IEC 23001-7] and ISO Base Media File Format Edition 4 [ISO/IEC 14496-12].</span></span>

#### <a name="2272-streammanifestbox"></a><span data-ttu-id="503cc-248">2.2.7.2 StreamManifestBox</span><span class="sxs-lookup"><span data-stu-id="503cc-248">2.2.7.2 StreamManifestBox</span></span> 

##### <a name="22721-streamsmil"></a><span data-ttu-id="503cc-249">2.2.7.2.1 StreamSMIL</span><span class="sxs-lookup"><span data-stu-id="503cc-249">2.2.7.2.1 StreamSMIL</span></span> 

#### <a name="2273-liveservermanifestbox"></a><span data-ttu-id="503cc-250">2.2.7.3 LiveServerManifestBox</span><span class="sxs-lookup"><span data-stu-id="503cc-250">2.2.7.3 LiveServerManifestBox</span></span> 

##### <a name="22731-livesmil"></a><span data-ttu-id="503cc-251">2.2.7.3.1 LiveSMIL</span><span class="sxs-lookup"><span data-stu-id="503cc-251">2.2.7.3.1 LiveSMIL</span></span> 

#### <a name="2274-moovbox"></a><span data-ttu-id="503cc-252">2.2.7.4 MoovBox</span><span class="sxs-lookup"><span data-stu-id="503cc-252">2.2.7.4 MoovBox</span></span> 

#### <a name="2275-fragment"></a><span data-ttu-id="503cc-253">2.2.7.5 Fragment</span><span class="sxs-lookup"><span data-stu-id="503cc-253">2.2.7.5 Fragment</span></span> 

##### <a name="22751-track-fragment-extended-header"></a><span data-ttu-id="503cc-254">2.2.7.5.1 Track Fragment Extended Header</span><span class="sxs-lookup"><span data-stu-id="503cc-254">2.2.7.5.1 Track Fragment Extended Header</span></span> 

### <a name="228-server-to-server-ingest"></a><span data-ttu-id="503cc-255">2.2.8 Server-to-Server Ingest</span><span class="sxs-lookup"><span data-stu-id="503cc-255">2.2.8 Server-to-Server Ingest</span></span> 

# <a name="3-protocol-details"></a><span data-ttu-id="503cc-256">3 Protocol Details</span><span class="sxs-lookup"><span data-stu-id="503cc-256">3 Protocol Details</span></span> 


## <a name="31-client-details"></a><span data-ttu-id="503cc-257">3.1 Client Details</span><span class="sxs-lookup"><span data-stu-id="503cc-257">3.1 Client Details</span></span> 

### <a name="311-abstract-data-model"></a><span data-ttu-id="503cc-258">3.1.1 Abstract Data Model</span><span class="sxs-lookup"><span data-stu-id="503cc-258">3.1.1 Abstract Data Model</span></span> 

#### <a name="3111-presentation-description"></a><span data-ttu-id="503cc-259">3.1.1.1 Presentation Description</span><span class="sxs-lookup"><span data-stu-id="503cc-259">3.1.1.1 Presentation Description</span></span> 

>   <span data-ttu-id="503cc-260">The Presentation Description data element encapsulates all metadata for the   presentation.</span><span class="sxs-lookup"><span data-stu-id="503cc-260">The Presentation Description data element encapsulates all metadata for the   presentation.</span></span>

>   <span data-ttu-id="503cc-261">Presentation Metadata: A set of metadata that is common to all streams in the presentation.</span><span class="sxs-lookup"><span data-stu-id="503cc-261">Presentation Metadata: A set of metadata that is common to all streams in the presentation.</span></span> <span data-ttu-id="503cc-262">Presentation Metadata comprises the following fields, specified in section *2.2.2.1*:</span><span class="sxs-lookup"><span data-stu-id="503cc-262">Presentation Metadata comprises the following fields, specified in section *2.2.2.1*:</span></span>

>   * <span data-ttu-id="503cc-263">**MajorVersion**</span><span class="sxs-lookup"><span data-stu-id="503cc-263">**MajorVersion**</span></span>
>   * <span data-ttu-id="503cc-264">**MinorVersion**</span><span class="sxs-lookup"><span data-stu-id="503cc-264">**MinorVersion**</span></span>
>   * <span data-ttu-id="503cc-265">**TimeScale**</span><span class="sxs-lookup"><span data-stu-id="503cc-265">**TimeScale**</span></span>
>   * <span data-ttu-id="503cc-266">**Duration**</span><span class="sxs-lookup"><span data-stu-id="503cc-266">**Duration**</span></span>
>   * <span data-ttu-id="503cc-267">**IsLive**</span><span class="sxs-lookup"><span data-stu-id="503cc-267">**IsLive**</span></span>
>   * <span data-ttu-id="503cc-268">**LookaheadCount**</span><span class="sxs-lookup"><span data-stu-id="503cc-268">**LookaheadCount**</span></span>
>   * <span data-ttu-id="503cc-269">**DVRWindowLength**</span><span class="sxs-lookup"><span data-stu-id="503cc-269">**DVRWindowLength**</span></span>

>   <span data-ttu-id="503cc-270">Presentations containing HEVC Streams SHALL set:</span><span class="sxs-lookup"><span data-stu-id="503cc-270">Presentations containing HEVC Streams SHALL set:</span></span>

    MajorVersion = 2
    MinorVersion = 2

>   <span data-ttu-id="503cc-271">LookaheadCount = 0 (Note: Boxes deprecated)</span><span class="sxs-lookup"><span data-stu-id="503cc-271">LookaheadCount = 0 (Note: Boxes deprecated)</span></span>

>   <span data-ttu-id="503cc-272">Presentations SHOULD also set:</span><span class="sxs-lookup"><span data-stu-id="503cc-272">Presentations SHOULD also set:</span></span>

    TimeScale = 90000

>   <span data-ttu-id="503cc-273">Stream Collection: A collection of Stream Description data elements, as   specified in section *3.1.1.1.2*.</span><span class="sxs-lookup"><span data-stu-id="503cc-273">Stream Collection: A collection of Stream Description data elements, as   specified in section *3.1.1.1.2*.</span></span>

>   <span data-ttu-id="503cc-274">Protection Description: A collection of Protection System Metadata   Description data elements, as specified in section *3.1.1.1.1*.</span><span class="sxs-lookup"><span data-stu-id="503cc-274">Protection Description: A collection of Protection System Metadata   Description data elements, as specified in section *3.1.1.1.1*.</span></span>

##### <a name="31111-protection-system-metadata-description"></a><span data-ttu-id="503cc-275">3.1.1.1.1 Protection System Metadata Description</span><span class="sxs-lookup"><span data-stu-id="503cc-275">3.1.1.1.1 Protection System Metadata Description</span></span> 

>   <span data-ttu-id="503cc-276">The Protection System Metadata Description data element encapsulates metadata specific to a single Content Protection System.</span><span class="sxs-lookup"><span data-stu-id="503cc-276">The Protection System Metadata Description data element encapsulates metadata specific to a single Content Protection System.</span></span> <span data-ttu-id="503cc-277">(No Change)</span><span class="sxs-lookup"><span data-stu-id="503cc-277">(No Change)</span></span>

>   <span data-ttu-id="503cc-278">Protection Header Description: Content protection metadata that pertains to a single Content Protection System.</span><span class="sxs-lookup"><span data-stu-id="503cc-278">Protection Header Description: Content protection metadata that pertains to a single Content Protection System.</span></span> <span data-ttu-id="503cc-279">Protection Header Description comprises the following fields, specified in section *2.2.2.2*:</span><span class="sxs-lookup"><span data-stu-id="503cc-279">Protection Header Description comprises the following fields, specified in section *2.2.2.2*:</span></span>

>   * <span data-ttu-id="503cc-280">**SystemID**</span><span class="sxs-lookup"><span data-stu-id="503cc-280">**SystemID**</span></span>
>   * <span data-ttu-id="503cc-281">**ProtectionHeaderContent**</span><span class="sxs-lookup"><span data-stu-id="503cc-281">**ProtectionHeaderContent**</span></span>

##### <a name="31112-stream-description"></a><span data-ttu-id="503cc-282">3.1.1.1.2 Stream Description</span><span class="sxs-lookup"><span data-stu-id="503cc-282">3.1.1.1.2 Stream Description</span></span> 

###### <a name="311121-track-description"></a><span data-ttu-id="503cc-283">3.1.1.1.2.1 Track Description</span><span class="sxs-lookup"><span data-stu-id="503cc-283">3.1.1.1.2.1 Track Description</span></span> 

###### <a name="3111211-custom-attribute-description"></a><span data-ttu-id="503cc-284">3.1.1.1.2.1.1 Custom Attribute Description</span><span class="sxs-lookup"><span data-stu-id="503cc-284">3.1.1.1.2.1.1 Custom Attribute Description</span></span> 

##### <a name="3113-fragment-reference-description"></a><span data-ttu-id="503cc-285">3.1.1.3 Fragment Reference Description</span><span class="sxs-lookup"><span data-stu-id="503cc-285">3.1.1.3 Fragment Reference Description</span></span> 

###### <a name="31131-track-specific-fragment-reference-description"></a><span data-ttu-id="503cc-286">3.1.1.3.1 Track-Specific Fragment Reference Description</span><span class="sxs-lookup"><span data-stu-id="503cc-286">3.1.1.3.1 Track-Specific Fragment Reference Description</span></span> 

#### <a name="3112-fragment-description"></a><span data-ttu-id="503cc-287">3.1.1.2 Fragment Description</span><span class="sxs-lookup"><span data-stu-id="503cc-287">3.1.1.2 Fragment Description</span></span> 

##### <a name="31121-sample-description"></a><span data-ttu-id="503cc-288">3.1.1.2.1 Sample Description</span><span class="sxs-lookup"><span data-stu-id="503cc-288">3.1.1.2.1 Sample Description</span></span> 

### <a name="312-timers"></a><span data-ttu-id="503cc-289">3.1.2 Timers</span><span class="sxs-lookup"><span data-stu-id="503cc-289">3.1.2 Timers</span></span> 

### <a name="313-initialization"></a><span data-ttu-id="503cc-290">3.1.3 Initialization</span><span class="sxs-lookup"><span data-stu-id="503cc-290">3.1.3 Initialization</span></span> 

### <a name="314-higher-layer-triggered-events"></a><span data-ttu-id="503cc-291">3.1.4 Higher-Layer Triggered Events</span><span class="sxs-lookup"><span data-stu-id="503cc-291">3.1.4 Higher-Layer Triggered Events</span></span> 

#### <a name="3141-open-presentation"></a><span data-ttu-id="503cc-292">3.1.4.1 Open Presentation</span><span class="sxs-lookup"><span data-stu-id="503cc-292">3.1.4.1 Open Presentation</span></span> 

#### <a name="3142-get-fragment"></a><span data-ttu-id="503cc-293">3.1.4.2 Get Fragment</span><span class="sxs-lookup"><span data-stu-id="503cc-293">3.1.4.2 Get Fragment</span></span> 

#### <a name="3143-close-presentation"></a><span data-ttu-id="503cc-294">3.1.4.3 Close Presentation</span><span class="sxs-lookup"><span data-stu-id="503cc-294">3.1.4.3 Close Presentation</span></span> 

### <a name="315-processing-events-and-sequencing-rules"></a><span data-ttu-id="503cc-295">3.1.5 Processing Events and Sequencing Rules</span><span class="sxs-lookup"><span data-stu-id="503cc-295">3.1.5 Processing Events and Sequencing Rules</span></span> 

#### <a name="3151-manifest-request-and-manifest-response"></a><span data-ttu-id="503cc-296">3.1.5.1 Manifest Request and Manifest Response</span><span class="sxs-lookup"><span data-stu-id="503cc-296">3.1.5.1 Manifest Request and Manifest Response</span></span> 

#### <a name="3152-fragment-request-and-fragment-response"></a><span data-ttu-id="503cc-297">3.1.5.2 Fragment Request and Fragment Response</span><span class="sxs-lookup"><span data-stu-id="503cc-297">3.1.5.2 Fragment Request and Fragment Response</span></span>

## <a name="32-server-details"></a><span data-ttu-id="503cc-298">3.2 Server Details</span><span class="sxs-lookup"><span data-stu-id="503cc-298">3.2 Server Details</span></span>

## <a name="33-live-encoder-details"></a><span data-ttu-id="503cc-299">3.3 Live Encoder Details</span><span class="sxs-lookup"><span data-stu-id="503cc-299">3.3 Live Encoder Details</span></span> 

# <a name="4-protocol-examples"></a><span data-ttu-id="503cc-300">4 Protocol Examples</span><span class="sxs-lookup"><span data-stu-id="503cc-300">4 Protocol Examples</span></span> 

# <a name="5-security"></a><span data-ttu-id="503cc-301">5 Security</span><span class="sxs-lookup"><span data-stu-id="503cc-301">5 Security</span></span> 

## <a name="51-security-considerations-for-implementers"></a><span data-ttu-id="503cc-302">5.1 Security Considerations for Implementers</span><span class="sxs-lookup"><span data-stu-id="503cc-302">5.1 Security Considerations for Implementers</span></span> 
-----------------------------------------

>   <span data-ttu-id="503cc-303">If the content transported using this protocol has high commercial value, a Content Protection System should be used to prevent unauthorized use of the content.</span><span class="sxs-lookup"><span data-stu-id="503cc-303">If the content transported using this protocol has high commercial value, a Content Protection System should be used to prevent unauthorized use of the content.</span></span> <span data-ttu-id="503cc-304">The **ProtectionElement** can be used to carry metadata related to the use of a Content Protection System.</span><span class="sxs-lookup"><span data-stu-id="503cc-304">The **ProtectionElement** can be used to carry metadata related to the use of a Content Protection System.</span></span> <span data-ttu-id="503cc-305">Protected audio and video content SHALL be encrypted as specified by MPEG Common Encryption Second Edition: 2015 [ISO/IEC 23001-7].</span><span class="sxs-lookup"><span data-stu-id="503cc-305">Protected audio and video content SHALL be encrypted as specified by MPEG Common Encryption Second Edition: 2015 [ISO/IEC 23001-7].</span></span>

>   <span data-ttu-id="503cc-306">**Note**: For HEVC video, only slice data in VCL NALs is encrypted.</span><span class="sxs-lookup"><span data-stu-id="503cc-306">**Note**: For HEVC video, only slice data in VCL NALs is encrypted.</span></span> <span data-ttu-id="503cc-307">Slice headers and other NALs are accessible to presentation applications prior to decryption.</span><span class="sxs-lookup"><span data-stu-id="503cc-307">Slice headers and other NALs are accessible to presentation applications prior to decryption.</span></span> <span data-ttu-id="503cc-308">in a secure video path, encrypted information is not available to presentation applications.</span><span class="sxs-lookup"><span data-stu-id="503cc-308">in a secure video path, encrypted information is not available to presentation applications.</span></span>

# <a name="52-index-of-security-parameters"></a><span data-ttu-id="503cc-309">5.2 Index of Security Parameters</span><span class="sxs-lookup"><span data-stu-id="503cc-309">5.2 Index of Security Parameters</span></span> 
-----------------------------


| <span data-ttu-id="503cc-310">**Security parameter**</span><span class="sxs-lookup"><span data-stu-id="503cc-310">**Security parameter**</span></span>  | <span data-ttu-id="503cc-311">**Section**</span><span class="sxs-lookup"><span data-stu-id="503cc-311">**Section**</span></span>         |
|-------------------------|---------------------|
| <span data-ttu-id="503cc-312">ProtectionElement</span><span class="sxs-lookup"><span data-stu-id="503cc-312">ProtectionElement</span></span>       | <span data-ttu-id="503cc-313">*2.2.2.2*</span><span class="sxs-lookup"><span data-stu-id="503cc-313">*2.2.2.2*</span></span>           |
| <span data-ttu-id="503cc-314">Common Encryption Boxes</span><span class="sxs-lookup"><span data-stu-id="503cc-314">Common Encryption Boxes</span></span> | <span data-ttu-id="503cc-315">*[ISO/IEC 23001-7]*</span><span class="sxs-lookup"><span data-stu-id="503cc-315">*[ISO/IEC 23001-7]*</span></span> |

# <a name="53-common-encryption-boxes"></a><span data-ttu-id="503cc-316">5.3 Common Encryption Boxes</span><span class="sxs-lookup"><span data-stu-id="503cc-316">5.3 Common Encryption Boxes</span></span>
-----------------------

<span data-ttu-id="503cc-317">The following boxes may be present in fragment responses when Common Encryption is applied, and are specified in [ISO/IEC 23001-7] or [ISO/IEC 14496-12]:</span><span class="sxs-lookup"><span data-stu-id="503cc-317">The following boxes may be present in fragment responses when Common Encryption is applied, and are specified in [ISO/IEC 23001-7] or [ISO/IEC 14496-12]:</span></span>

1.  <span data-ttu-id="503cc-318">Protection System Specific Header Box (‘pssh’)</span><span class="sxs-lookup"><span data-stu-id="503cc-318">Protection System Specific Header Box (‘pssh’)</span></span>

2.  <span data-ttu-id="503cc-319">Sample Encryption Box (‘senc’)</span><span class="sxs-lookup"><span data-stu-id="503cc-319">Sample Encryption Box (‘senc’)</span></span>

3.  <span data-ttu-id="503cc-320">Sample Auxiliary Information Offset Box (‘saio’)</span><span class="sxs-lookup"><span data-stu-id="503cc-320">Sample Auxiliary Information Offset Box (‘saio’)</span></span>

4.  <span data-ttu-id="503cc-321">Sample Auxiliary Information Size Box (‘saiz’)</span><span class="sxs-lookup"><span data-stu-id="503cc-321">Sample Auxiliary Information Size Box (‘saiz’)</span></span>

5.  <span data-ttu-id="503cc-322">Sample Group Description Box (‘sgpd’)</span><span class="sxs-lookup"><span data-stu-id="503cc-322">Sample Group Description Box (‘sgpd’)</span></span>

6.  <span data-ttu-id="503cc-323">Sample to Group Box (‘sbgp’)</span><span class="sxs-lookup"><span data-stu-id="503cc-323">Sample to Group Box (‘sbgp’)</span></span>

-----------------------

## <a name="media-services-learning-paths"></a><span data-ttu-id="503cc-324">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="503cc-324">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="503cc-325">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="503cc-325">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

[image1]: ./media/media-services-fmp4-live-ingest-overview/media-services-image1.png
[image2]: ./media/media-services-fmp4-live-ingest-overview/media-services-image2.png
[image3]: ./media/media-services-fmp4-live-ingest-overview/media-services-image3.png
[image4]: ./media/media-services-fmp4-live-ingest-overview/media-services-image4.png
[image5]: ./media/media-services-fmp4-live-ingest-overview/media-services-image5.png
[image6]: ./media/media-services-fmp4-live-ingest-overview/media-services-image6.png
[image7]: ./media/media-services-fmp4-live-ingest-overview/media-services-image7.png
