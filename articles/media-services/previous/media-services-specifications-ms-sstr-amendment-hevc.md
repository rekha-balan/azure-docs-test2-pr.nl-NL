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
# <a name="smooth-streaming-protocol-ms-sstr-amendment-for-hevc"></a>Smooth Streaming Protocol (MS-SSTR) Amendment for HEVC

## <a name="1-introduction"></a>1 Introduction 

This article provides detailed amendments to be applied to the Smooth Streaming Protocol specification [MS-SSTR] to enable Smooth Streaming of HEVC encoded video. In this specification, we outline only the changes required to deliver the HEVC video codec. The article follows the same numbering schema as the [MS-SSTR] specification. The empty headlines presented throughout the article are provided to orient the reader to their position in the [MS-SSTR] specification.  “(No Change)” indicates text is copied for clarification purposes only.

The article provides technical implementation requirements for the signaling of HEVC video codec in a Smooth Streaming manifest and normative  references are updated to reference the current MPEG standards that include HEVC, Common Encryption of HEVC, and box names for ISO Base Media File Format have been updated to be consistent with the latest specifications. 

The referenced Smooth Streaming Protocol specification [MS-SSTR] describes the wire format used to deliver live and on-demand digital media, such as audio and video, in the following manners: from an encoder to a web server, from a server to another server, and from a server to an HTTP client.
The use of an MPEG-4 ([[MPEG4-RA])](http://go.microsoft.com/fwlink/?LinkId=327787)-based data structure delivery over HTTP allows seamless switching in near real time between different quality levels of compressed media content. The result is a constant playback experience for the HTTP client end user, even if network and video rendering conditions change for the client computer or device.

## <a name="11-glossary"></a>1.1 Glossary 

The following terms are defined in *[MS-GLOS]*:

>   **globally unique identifier (GUID) universally unique identifier (UUID)**

The following terms are specific to this document:

>  **composition time:** The time a sample is presented at the client,   as defined in   [[ISO/IEC-14496-12].](http://go.microsoft.com/fwlink/?LinkId=183695)

>   **CENC**: Common Encryption, as defined in [ISO/IEC 23001-7] Second Edition.

>   **decode time:** The time a sample is required to be decoded on the client,   as defined in   [[ISO/IEChttp://go.microsoft.com/fwlink/?LinkId=18369514496-12].](http://go.microsoft.com/fwlink/?LinkId=183695)

**fragment:** An independently downloadable unit of **media** that comprises one or more **samples**.

>   **HEVC:** High Efficiency Video Coding, as defined in [ISO/IEC 23008-2]

>   **manifest:** Metadata about the **presentation** that allows a client to make requests for **media**. **media:** Compressed audio, video, and text data used by the client to play a **presentation**. **media format:** A well-defined format for representing audio or video as a compressed **sample**.

>   **presentation:** The set of all **streams** and related metadata needed to play a single movie. **request:** An HTTP message sent from the client to the server, as defined in [[RFC2616].](http://go.microsoft.com/fwlink/?LinkId=90372) **response:** An HTTP message sent from the server to the client, as defined in [[RFC2616].](http://go.microsoft.com/fwlink/?LinkId=90372)

>   **sample:** The smallest fundamental unit (such as a frame) in which   **media** is stored and processed.

>   **MAY, SHOULD, MUST, SHOULD NOT, MUST NOT:** These terms (in all caps) are used as described in [[RFC2119].](http://go.microsoft.com/fwlink/?LinkId=90317) All statements of optional behavior use either MAY, SHOULD, or SHOULD NOT.

## <a name="12-references"></a>1.2 References 
-----------

>   References to Microsoft Open Specifications documentation do not include a publishing year because links are to the latest version of the documents, which are updated frequently. References to other documents include a publishing year when one is available.

 ### <a name="121-normative-references"></a>1.2.1 Normative References 

>  [MS-SSTR] Smooth Streaming Protocol *v20140502* [http://download.microsoft.com/download/9/5/E/95EF66AF-9026-4BB0-A41D-A4F81802D92C/[MS-SSTR].pdf](http://download.microsoft.com/download/9/5/E/95EF66AF-9026-4BB0-A41D-A4F81802D92C/%5bMS-SSTR%5d.pdf)

>   [ISO/IEC 14496-12] International Organization for Standardization, "Information technology -- Coding of audio-visual objects -- Part 12: ISO Base Media File Format", ISO/IEC 14496-12:2014, Edition 4, Plus Corrigendum 1, Amendments 1 & 2.
>   <http://standards.iso.org/ittf/PubliclyAvailableStandards/c061988_ISO_IEC_14496-12_2012.zip>

>   [ISO/IEC 14496-15] International Organization for Standardization, "Information technology -- Coding of audio-visual objects -- Part 15: Carriage of NAL unit structured video in the ISO Base Media File Format", ISO 14496-15:2015, Edition 3.
>   <http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=65216>

>   [ISO/IEC 23008-2] Information technology -- High efficiency coding and media   delivery in heterogeneous environments -- Part 2: High efficiency video   coding: 2013 or newest edition   <http://standards.iso.org/ittf/PubliclyAvailableStandards/c035424_ISO_IEC_23008-2_2013.zip>

>   [ISO/IEC 23001-7] Information technology — MPEG systems technologies — Part   7: Common encryption in ISO base media file format files, CENC Edition   2:2015 <http://www.iso.org/iso/catalogue_detail.htm?csnumber=65271>

>   [RFC-6381] IETF RFC-6381, “The 'Codecs' and 'Profiles' Parameters for   "Bucket" Media Types” <http://tools.ietf.org/html/rfc6381>

>   [MPEG4-RA] The MP4 Registration Authority, "MP4REG", [http://www.mp4ra.org   ](http://go.microsoft.com/fwlink/?LinkId=327787)

>   [RFC2119] Bradner, S., "Key words for use in RFCs to Indicate Requirement   Levels", BCP 14, RFC 2119, March 1997,   [http://www.rfc-editor.org/rfc/rfc2119.txt   ](http://go.microsoft.com/fwlink/?LinkId=90317)

### <a name="122-informative-references"></a>1.2.2 Informative References 

>   [MS-GLOS] Microsoft Corporation, "*Windows Protocols Master Glossary*."

>   [RFC3548] Josefsson, S., Ed., "The Base16, Base32, and Base64 Data   Encodings", RFC 3548, July 2003, [http://www.ietf.org/rfc/rfc3548.txt   ](http://go.microsoft.com/fwlink/?LinkId=90432)

>   [RFC5234] Crocker, D., Ed., and Overell, P., "Augmented BNF for Syntax   Specifications: ABNF", STD 68, RFC 5234, January 2008,   [http://www.rfc-editor.org/rfc/rfc5234.txt   ](http://go.microsoft.com/fwlink/?LinkId=123096)


## <a name="13-overview"></a>1.3 Overview 
---------

>   Only changes to the Smooth Streaming specification required for the delivery of HEVC are specified below. Unchanged section headers are listed to maintain location in the referenced Smooth Streaming specification [MS-SSTR].

## <a name="14-relationship-to-other-protocols"></a>1.4 Relationship to Other Protocols 
--------------------------------

## <a name="15-prerequisitespreconditions"></a>1.5 Prerequisites/Preconditions 
----------------------------

## <a name="16-applicability-statement"></a>1.6 Applicability Statement 
------------------------

## <a name="17-versioning-and-capability-negotiation"></a>1.7 Versioning and Capability Negotiation 
--------------------------------------

## <a name="18-vendor-extensible-fields"></a>1.8 Vendor-Extensible Fields 
-------------------------

>   The following method SHALL be used identify streams using the HEVC video   format:

>   * **Custom Descriptive Codes for Media Formats:** This capability is provided by the **FourCC** field, as specified in section *2.2.2.5*.
>   Implementers can ensure that extensions do not conflict by registering extension codes with the MPEG4-RA, as specified in [[ISO/IEC-14496-12] ](http://go.microsoft.com/fwlink/?LinkId=183695)

## <a name="19-standards-assignments"></a>1.9 Standards Assignments 
----------------------

# <a name="2-messages"></a>2 Messages 

## <a name="21-transport"></a>2.1 Transport 
----------

## <a name="22-message-syntax"></a>2.2 Message Syntax 
---------------

### <a name="221-manifest-request"></a>2.2.1 Manifest Request 

### <a name="222-manifest-response"></a>2.2.2 Manifest Response 

#### <a name="2221-smoothstreamingmedia"></a>2.2.2.1 SmoothStreamingMedia 

>   **MinorVersion (variable):** The minor version of the Manifest Response message. MUST be set to 2. (No Change)

>   **TimeScale (variable):** The time scale of the Duration attribute, specified as the number of increments in one second. The default value is
>   10000000. (No Change)

>   The recommended value is 90000 for representing the exact duration of video   frames and fragments containing fractional framerate video (for example, 30/1.001   Hz).

#### <a name="2222-protectionelement"></a>2.2.2.2 ProtectionElement 

The ProtectionElement SHALL be present when Common Encryption (CENC) has been applied to video or audio streams. HEVC encrypted streams SHALL conform to Common Encryption 2nd Edition [ISO/IEC 23001-7]. Only slice data in VCL NAL Units SHALL be encrypted.

#### <a name="2223-streamelement"></a>2.2.2.3 StreamElement 

>   **StreamTimeScale (variable):** The time scale for duration and time values in this stream, specified as the number of increments in one second. A value of 90000 is recommended for HEVC streams. A value matching the waveform sample frequency (for example, 48000 or 44100) is recommended for audio streams.

##### <a name="22231-streamprotectionelement"></a>2.2.2.3.1 StreamProtectionElement

#### <a name="2224-urlpattern"></a>2.2.2.4 UrlPattern 

#### <a name="225-trackelement"></a>2.2.5 TrackElement 

>   **FourCC (variable):** A four-character code that identifies which media format is used for each sample. The following range of values is reserved with the following semantic meanings:

>  * "hev1”: Video samples for this track use HEVC video, using the ‘hev1’ sample description format specified in [ISO/IEC-14496-15].

>   **CodecPrivateData (variable):** Data that specifies parameters specific to the media format and common to all samples in the track, represented as a string of hex-coded bytes. The format and semantic meaning of byte sequence varies with the value of the **FourCC** field as follows:

>   * When a TrackElement describes HEVC video, the **FourCC** field SHALL equal **"hev1"** and;

>   The **CodecPrivateData** field SHALL contain a hex-coded string   representation of the following byte sequence, specified in ABNF   [[RFC5234]:](http://go.microsoft.com/fwlink/?LinkId=123096) (no change from   MS-SSTR)

>   * %x00 %x00 %x00 %x01 SPSField %x00 %x00 %x00 %x01 PPSField

>   * SPSField contains the Sequence Parameter Set (SPS).

>   * PPSField contains the Slice Parameter Set (PPS).

>   Note: The Video Parameter Set (VPS) is not contained in CodecPrivateData, but should be contained in the file header of stored files in the ‘hvcC’ box. Systems using Smooth Streaming Protocol must signal additional decoding parameters (for example, HEVC Tier) using the Custom Attribute “codecs.”

##### <a name="22251-customattributeselement"></a>2.2.2.5.1 CustomAttributesElement 

#### <a name="226-streamfragmentelement"></a>2.2.6 StreamFragmentElement 

>   The **SmoothStreamingMedia’s MajorVersion** field MUST be set to 2, and **MinorVersion** field MUST be set to 2. (No Change)

##### <a name="22261-trackfragmentelement"></a>2.2.2.6.1 TrackFragmentElement 

### <a name="223-fragment-request"></a>2.2.3 Fragment Request 

>   **Note**: The default media format requested for **MinorVersion** 2 and ‘hev1’   is ‘iso8’ brand ISO Base Media File Format specified in [ISO/IEC 14496-12]   ISO Base Media File Format Fourth Edition, and [ISO/IEC 23001-7] Common   Encryption Second Edition.

### <a name="224-fragment-response"></a>2.2.4 Fragment Response 

#### <a name="2241-moofbox"></a>2.2.4.1 MoofBox 

#### <a name="2242-mfhdbox"></a>2.2.4.2 MfhdBox 

#### <a name="2243-trafbox"></a>2.2.4.3 TrafBox 

#### <a name="2244-tfxdbox"></a>2.2.4.4 TfxdBox 

>   The **TfxdBox** is deprecated, and its function replaced by the Track   Fragment Decode Time Box (‘tfdt’) specified in [ISO/IEC 14496-12] section   8.8.12.

>   **Note**: A client may calculate the duration of a fragment by summing the sample durations listed in the Track Run Box (‘trun’) or multiplying the number of samples times the default sample duration. The baseMediaDecodeTime in ‘tfdt’ plus fragment duration equals the URL time parameter for the next fragment.

>   A Producer Reference Time Box (‘prft’) SHOULD be inserted prior to a Movie   Fragment Box (‘moof’) as needed, to indicate the UTC time corresponding to   the Track Fragment Decode Time of the first sample referenced by the Movie   Fragment Box, as specified in [ISO/IEC 14496-12] section 8.16.5.

#### <a name="2245-tfrfbox"></a>2.2.4.5 TfrfBox 

>   The **TfrfBox** is deprecated, and its function replaced by the Track   Fragment Decode Time Box (‘tfdt’) specified in [ISO/IEC 14496-12] section   8.8.12.

>   **Note**: A client may calculate the duration of a fragment by summing the sample durations listed in the Track Run Box (‘trun’) or multiplying the number of samples times the default sample duration. The baseMediaDecodeTime in ‘tfdt’ plus fragment duration equals the URL time parameter for the next fragment. Look ahead addresses are deprecated because they delay live streaming.

#### <a name="2246-tfhdbox"></a>2.2.4.6 TfhdBox 

>   The **TfhdBox** and related fields encapsulate defaults for per sample metadata in the fragment. The syntax of the **TfhdBox** field is a strict subset of the syntax of the Track Fragment Header Box defined in [[ISO/IEC-14496-12]](http://go.microsoft.com/fwlink/?LinkId=183695) section 8.8.7.

>   **BaseDataOffset (8 bytes):** The offset, in bytes, from the beginning of the **MdatBox** field to the sample field in the **MdatBox** field. To signal this restriction, the default-base-is-moof flag (0x020000) must be set.

#### <a name="2247-trunbox"></a>2.2.4.7 TrunBox 

>   The **TrunBox** and related fields encapsulate per sample metadata for the requested fragment. The syntax of **TrunBox** is a strict subset of the Version 1 Track Fragment Run Box defined in [[ISO/IEC-14496-](http://go.microsoft.com/fwlink/?LinkId=183695)*12]* section 8.8.8.

>   **SampleCompositionTimeOffset (4 bytes):** The Sample Composition Time offset of each sample adjusted so that the presentation time of the first presented sample in the fragment is equal to the decode time of the first decoded sample. Negative video sample composition offsets SHALL be used,

>   as defined in   [[ISO/IEC-14496-12].](http://go.microsoft.com/fwlink/?LinkId=183695)

>   Note: This avoids a video synchronization error caused by video lagging   audio equal to the largest decoded picture buffer removal delay, and   maintains presentation timing between alternative fragments that may have   different removal delays.

>   The syntax of the fields defined in this section, specified in ABNF   [[RFC5234],](http://go.microsoft.com/fwlink/?LinkId=123096) remains the   same, except as follows:

>   SampleCompositionTimeOffset = SIGNED_INT32

#### <a name="2248-mdatbox"></a>2.2.4.8 MdatBox 

#### <a name="2249-fragment-response-common-fields"></a>2.2.4.9 Fragment Response Common Fields 

### <a name="225-sparse-stream-pointer"></a>2.2.5 Sparse Stream Pointer 

### <a name="226-fragment-not-yet-available"></a>2.2.6 Fragment Not Yet Available 

### <a name="227-live-ingest"></a>2.2.7 Live Ingest 

#### <a name="2271-filetype"></a>2.2.7.1 FileType 

>   **FileType (variable):** specifies the subtype and intended use of the   MPEG-4 ([[MPEG4-RA])](http://go.microsoft.com/fwlink/?LinkId=327787) file,   and high-level attributes.

>   **MajorBrand (variable):** The major brand of the media file. MUST be set to "isml."

>   **MinorVersion (variable):** The minor version of the media file. MUST be set to 1.

>   **CompatibleBrands (variable):** Specifies the supported brands of MPEG-4.
>   MUST include "ccff" and "iso8."

>   The syntax of the fields defined in this section, specified in ABNF   [[RFC5234],](http://go.microsoft.com/fwlink/?LinkId=123096) is as follows:

    FileType = MajorBrand MinorVersion CompatibleBrands
    MajorBrand = STRING_UINT32
    MinorVersion = STRING_UINT32
    CompatibleBrands = "ccff" "iso8" 0\*(STRING_UINT32)

**Note**: The compatibility brands ‘ccff’ and ‘iso8’ indicate that fragments conform to “Common Container File Format” and Common Encryption [ISO/IEC 23001-7] and ISO Base Media File Format Edition 4 [ISO/IEC 14496-12].

#### <a name="2272-streammanifestbox"></a>2.2.7.2 StreamManifestBox 

##### <a name="22721-streamsmil"></a>2.2.7.2.1 StreamSMIL 

#### <a name="2273-liveservermanifestbox"></a>2.2.7.3 LiveServerManifestBox 

##### <a name="22731-livesmil"></a>2.2.7.3.1 LiveSMIL 

#### <a name="2274-moovbox"></a>2.2.7.4 MoovBox 

#### <a name="2275-fragment"></a>2.2.7.5 Fragment 

##### <a name="22751-track-fragment-extended-header"></a>2.2.7.5.1 Track Fragment Extended Header 

### <a name="228-server-to-server-ingest"></a>2.2.8 Server-to-Server Ingest 

# <a name="3-protocol-details"></a>3 Protocol Details 


## <a name="31-client-details"></a>3.1 Client Details 

### <a name="311-abstract-data-model"></a>3.1.1 Abstract Data Model 

#### <a name="3111-presentation-description"></a>3.1.1.1 Presentation Description 

>   The Presentation Description data element encapsulates all metadata for the   presentation.

>   Presentation Metadata: A set of metadata that is common to all streams in the presentation. Presentation Metadata comprises the following fields, specified in section *2.2.2.1*:

>   * **MajorVersion**
>   * **MinorVersion**
>   * **TimeScale**
>   * **Duration**
>   * **IsLive**
>   * **LookaheadCount**
>   * **DVRWindowLength**

>   Presentations containing HEVC Streams SHALL set:

    MajorVersion = 2
    MinorVersion = 2

>   LookaheadCount = 0 (Note: Boxes deprecated)

>   Presentations SHOULD also set:

    TimeScale = 90000

>   Stream Collection: A collection of Stream Description data elements, as   specified in section *3.1.1.1.2*.

>   Protection Description: A collection of Protection System Metadata   Description data elements, as specified in section *3.1.1.1.1*.

##### <a name="31111-protection-system-metadata-description"></a>3.1.1.1.1 Protection System Metadata Description 

>   The Protection System Metadata Description data element encapsulates metadata specific to a single Content Protection System. (No Change)

>   Protection Header Description: Content protection metadata that pertains to a single Content Protection System. Protection Header Description comprises the following fields, specified in section *2.2.2.2*:

>   * **SystemID**
>   * **ProtectionHeaderContent**

##### <a name="31112-stream-description"></a>3.1.1.1.2 Stream Description 

###### <a name="311121-track-description"></a>3.1.1.1.2.1 Track Description 

###### <a name="3111211-custom-attribute-description"></a>3.1.1.1.2.1.1 Custom Attribute Description 

##### <a name="3113-fragment-reference-description"></a>3.1.1.3 Fragment Reference Description 

###### <a name="31131-track-specific-fragment-reference-description"></a>3.1.1.3.1 Track-Specific Fragment Reference Description 

#### <a name="3112-fragment-description"></a>3.1.1.2 Fragment Description 

##### <a name="31121-sample-description"></a>3.1.1.2.1 Sample Description 

### <a name="312-timers"></a>3.1.2 Timers 

### <a name="313-initialization"></a>3.1.3 Initialization 

### <a name="314-higher-layer-triggered-events"></a>3.1.4 Higher-Layer Triggered Events 

#### <a name="3141-open-presentation"></a>3.1.4.1 Open Presentation 

#### <a name="3142-get-fragment"></a>3.1.4.2 Get Fragment 

#### <a name="3143-close-presentation"></a>3.1.4.3 Close Presentation 

### <a name="315-processing-events-and-sequencing-rules"></a>3.1.5 Processing Events and Sequencing Rules 

#### <a name="3151-manifest-request-and-manifest-response"></a>3.1.5.1 Manifest Request and Manifest Response 

#### <a name="3152-fragment-request-and-fragment-response"></a>3.1.5.2 Fragment Request and Fragment Response

## <a name="32-server-details"></a>3.2 Server Details

## <a name="33-live-encoder-details"></a>3.3 Live Encoder Details 

# <a name="4-protocol-examples"></a>4 Protocol Examples 

# <a name="5-security"></a>5 Security 

## <a name="51-security-considerations-for-implementers"></a>5.1 Security Considerations for Implementers 
-----------------------------------------

>   If the content transported using this protocol has high commercial value, a Content Protection System should be used to prevent unauthorized use of the content. The **ProtectionElement** can be used to carry metadata related to the use of a Content Protection System. Protected audio and video content SHALL be encrypted as specified by MPEG Common Encryption Second Edition: 2015 [ISO/IEC 23001-7].

>   **Note**: For HEVC video, only slice data in VCL NALs is encrypted. Slice headers and other NALs are accessible to presentation applications prior to decryption. in a secure video path, encrypted information is not available to presentation applications.

# <a name="52-index-of-security-parameters"></a>5.2 Index of Security Parameters 
-----------------------------


| **Security parameter**  | **Section**         |
|-------------------------|---------------------|
| ProtectionElement       | *2.2.2.2*           |
| Common Encryption Boxes | *[ISO/IEC 23001-7]* |

# <a name="53-common-encryption-boxes"></a>5.3 Common Encryption Boxes
-----------------------

The following boxes may be present in fragment responses when Common Encryption is applied, and are specified in [ISO/IEC 23001-7] or [ISO/IEC 14496-12]:

1.  Protection System Specific Header Box (‘pssh’)

2.  Sample Encryption Box (‘senc’)

3.  Sample Auxiliary Information Offset Box (‘saio’)

4.  Sample Auxiliary Information Size Box (‘saiz’)

5.  Sample Group Description Box (‘sgpd’)

6.  Sample to Group Box (‘sbgp’)

-----------------------

## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

[image1]: ./media/media-services-fmp4-live-ingest-overview/media-services-image1.png
[image2]: ./media/media-services-fmp4-live-ingest-overview/media-services-image2.png
[image3]: ./media/media-services-fmp4-live-ingest-overview/media-services-image3.png
[image4]: ./media/media-services-fmp4-live-ingest-overview/media-services-image4.png
[image5]: ./media/media-services-fmp4-live-ingest-overview/media-services-image5.png
[image6]: ./media/media-services-fmp4-live-ingest-overview/media-services-image6.png
[image7]: ./media/media-services-fmp4-live-ingest-overview/media-services-image7.png
