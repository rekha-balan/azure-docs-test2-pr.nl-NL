---
title: Azure Media Services with PlayReady license template
description: This topic gives an overview of a PlayReady license template that is used to configure PlayReady licenses.
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
ms.date: 07/08/2018
ms.author: juliako
ms.openlocfilehash: d5315c6cc4ade94bc829aa77f795d9688f78b0ec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865881"
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="c0864-103">Media Services PlayReady license template overview</span><span class="sxs-lookup"><span data-stu-id="c0864-103">Media Services PlayReady license template overview</span></span> 

<span data-ttu-id="c0864-104">Azure Media Services enables you to encrypt your content with **Microsoft PlayReady**.</span><span class="sxs-lookup"><span data-stu-id="c0864-104">Azure Media Services enables you to encrypt your content with **Microsoft PlayReady**.</span></span> <span data-ttu-id="c0864-105">Media Services also provides a service for delivering PlayReady licenses.</span><span class="sxs-lookup"><span data-stu-id="c0864-105">Media Services also provides a service for delivering PlayReady licenses.</span></span> <span data-ttu-id="c0864-106">You can use Media Services APIs to configure PlayReady licenses.</span><span class="sxs-lookup"><span data-stu-id="c0864-106">You can use Media Services APIs to configure PlayReady licenses.</span></span> <span data-ttu-id="c0864-107">When a player tries to play your PlayReady-protected content, a request is sent to the license delivery service to obtain a license.</span><span class="sxs-lookup"><span data-stu-id="c0864-107">When a player tries to play your PlayReady-protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="c0864-108">If the license service approves the request, it issues the license that is sent to the client and is used to decrypt and play the specified content.</span><span class="sxs-lookup"><span data-stu-id="c0864-108">If the license service approves the request, it issues the license that is sent to the client and is used to decrypt and play the specified content.</span></span>

<span data-ttu-id="c0864-109">PlayReady licenses contain the rights and restrictions that you want the PlayReady digital rights management (DRM) runtime to enforce when a user tries to play back protected content.</span><span class="sxs-lookup"><span data-stu-id="c0864-109">PlayReady licenses contain the rights and restrictions that you want the PlayReady digital rights management (DRM) runtime to enforce when a user tries to play back protected content.</span></span> <span data-ttu-id="c0864-110">Here are some examples of PlayReady license restrictions that you can specify:</span><span class="sxs-lookup"><span data-stu-id="c0864-110">Here are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="c0864-111">The date and time from which the license is valid.</span><span class="sxs-lookup"><span data-stu-id="c0864-111">The date and time from which the license is valid.</span></span>
* <span data-ttu-id="c0864-112">The DateTime value when the license expires.</span><span class="sxs-lookup"><span data-stu-id="c0864-112">The DateTime value when the license expires.</span></span> 
* <span data-ttu-id="c0864-113">For the license to be saved in persistent storage on the client.</span><span class="sxs-lookup"><span data-stu-id="c0864-113">For the license to be saved in persistent storage on the client.</span></span> <span data-ttu-id="c0864-114">Persistent licenses are typically used to allow offline playback of the content.</span><span class="sxs-lookup"><span data-stu-id="c0864-114">Persistent licenses are typically used to allow offline playback of the content.</span></span>
* <span data-ttu-id="c0864-115">The minimum security level that a player must have to play your content.</span><span class="sxs-lookup"><span data-stu-id="c0864-115">The minimum security level that a player must have to play your content.</span></span> 
* <span data-ttu-id="c0864-116">The output protection level for the output controls for audio\video content.</span><span class="sxs-lookup"><span data-stu-id="c0864-116">The output protection level for the output controls for audio\video content.</span></span> 
* <span data-ttu-id="c0864-117">For more information, see the "Output Controls" section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span><span class="sxs-lookup"><span data-stu-id="c0864-117">For more information, see the "Output Controls" section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="c0864-118">Currently, you can only configure the PlayRight of the PlayReady license.</span><span class="sxs-lookup"><span data-stu-id="c0864-118">Currently, you can only configure the PlayRight of the PlayReady license.</span></span> <span data-ttu-id="c0864-119">This right is required.</span><span class="sxs-lookup"><span data-stu-id="c0864-119">This right is required.</span></span> <span data-ttu-id="c0864-120">The PlayRight gives the client the ability to play back the content.</span><span class="sxs-lookup"><span data-stu-id="c0864-120">The PlayRight gives the client the ability to play back the content.</span></span> <span data-ttu-id="c0864-121">You also can use the PlayRight to configure restrictions specific to playback.</span><span class="sxs-lookup"><span data-stu-id="c0864-121">You also can use the PlayRight to configure restrictions specific to playback.</span></span> 
> 

<span data-ttu-id="c0864-122">This topic describes how to configure PlayReady licenses with  Media Services.</span><span class="sxs-lookup"><span data-stu-id="c0864-122">This topic describes how to configure PlayReady licenses with  Media Services.</span></span>

## <a name="basic-streaming-license-example"></a><span data-ttu-id="c0864-123">Basic streaming license example</span><span class="sxs-lookup"><span data-stu-id="c0864-123">Basic streaming license example</span></span>

<span data-ttu-id="c0864-124">The following example shows the simplest (and most common) template that configures a basic streaming license.</span><span class="sxs-lookup"><span data-stu-id="c0864-124">The following example shows the simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="c0864-125">With this license, your clients can play back your PlayReady-protected content.</span><span class="sxs-lookup"><span data-stu-id="c0864-125">With this license, your clients can play back your PlayReady-protected content.</span></span> 

<span data-ttu-id="c0864-126">The XML conforms to the PlayReady license template XML schema defined in the [PlayReady license template XML schema](#schema) section.</span><span class="sxs-lookup"><span data-stu-id="c0864-126">The XML conforms to the PlayReady license template XML schema defined in the [PlayReady license template XML schema](#schema) section.</span></span>


    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>


## <a id="classes"></a><span data-ttu-id="c0864-127">Use Media Services APIs to configure license templates</span><span class="sxs-lookup"><span data-stu-id="c0864-127">Use Media Services APIs to configure license templates</span></span>

<span data-ttu-id="c0864-128">Media Services provides types that you can use to configure a PlayReady license template.</span><span class="sxs-lookup"><span data-stu-id="c0864-128">Media Services provides types that you can use to configure a PlayReady license template.</span></span> 

<span data-ttu-id="c0864-129">The snippet that follows uses Media Services .NET classes to configure the PlayReady license template.</span><span class="sxs-lookup"><span data-stu-id="c0864-129">The snippet that follows uses Media Services .NET classes to configure the PlayReady license template.</span></span> <span data-ttu-id="c0864-130">The classes are defined in the [Microsoft.Azure.Management.Media.Models](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.media.models?view=azure-dotnet) namespace.</span><span class="sxs-lookup"><span data-stu-id="c0864-130">The classes are defined in the [Microsoft.Azure.Management.Media.Models](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.media.models?view=azure-dotnet) namespace.</span></span> <span data-ttu-id="c0864-131">The snippet configures the PlayRight of the PlayReady license.</span><span class="sxs-lookup"><span data-stu-id="c0864-131">The snippet configures the PlayRight of the PlayReady license.</span></span> <span data-ttu-id="c0864-132">PlayRight grants the user the ability to play back the content subject to any restrictions configured in the license and on the PlayRight itself (for playback-specific policy).</span><span class="sxs-lookup"><span data-stu-id="c0864-132">PlayRight grants the user the ability to play back the content subject to any restrictions configured in the license and on the PlayRight itself (for playback-specific policy).</span></span> <span data-ttu-id="c0864-133">Much of the policy on a PlayRight concerns output restriction that control the types of outputs that the content can be played over.</span><span class="sxs-lookup"><span data-stu-id="c0864-133">Much of the policy on a PlayRight concerns output restriction that control the types of outputs that the content can be played over.</span></span> <span data-ttu-id="c0864-134">It also includes any restrictions that must be put in place when a given output is used.</span><span class="sxs-lookup"><span data-stu-id="c0864-134">It also includes any restrictions that must be put in place when a given output is used.</span></span> <span data-ttu-id="c0864-135">For example, if DigitalVideoOnlyContentRestriction is enabled, the DRM runtime only allows the video to be displayed over digital outputs.</span><span class="sxs-lookup"><span data-stu-id="c0864-135">For example, if DigitalVideoOnlyContentRestriction is enabled, the DRM runtime only allows the video to be displayed over digital outputs.</span></span> <span data-ttu-id="c0864-136">(Analog video outputs aren't allowed to pass the content.)</span><span class="sxs-lookup"><span data-stu-id="c0864-136">(Analog video outputs aren't allowed to pass the content.)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0864-137">PlayReady license has restrictions that are powerful.</span><span class="sxs-lookup"><span data-stu-id="c0864-137">PlayReady license has restrictions that are powerful.</span></span> <span data-ttu-id="c0864-138">If the output protections are too restrictive, the content might be unplayable on some clients.</span><span class="sxs-lookup"><span data-stu-id="c0864-138">If the output protections are too restrictive, the content might be unplayable on some clients.</span></span> <span data-ttu-id="c0864-139">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/).</span><span class="sxs-lookup"><span data-stu-id="c0864-139">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/).</span></span>

### <a name="configure-playready-license-template-with-net"></a><span data-ttu-id="c0864-140">Configure PlayReady license template with .NET</span><span class="sxs-lookup"><span data-stu-id="c0864-140">Configure PlayReady license template with .NET</span></span>

```csharp
ContentKeyPolicyPlayReadyLicense objContentKeyPolicyPlayReadyLicense;
objContentKeyPolicyPlayReadyLicense = new ContentKeyPolicyPlayReadyLicense
{
    AllowTestDevices = true,
    BeginDate = new DateTime(2016, 1, 1),
    ContentKeyLocation = new ContentKeyPolicyPlayReadyContentEncryptionKeyFromHeader(),
    ContentType = ContentKeyPolicyPlayReadyContentType.UltraVioletStreaming,
    LicenseType = drmSettings.EnbleOfflineMode ? ContentKeyPolicyPlayReadyLicenseType.Persistent : ContentKeyPolicyPlayReadyLicenseType.NonPersistent,
    PlayRight = new ContentKeyPolicyPlayReadyPlayRight
    {
        ImageConstraintForAnalogComponentVideoRestriction = true,
        ExplicitAnalogTelevisionOutputRestriction = new ContentKeyPolicyPlayReadyExplicitAnalogTelevisionRestriction(true, 2),
        AllowPassingVideoContentToUnknownOutput = ContentKeyPolicyPlayReadyUnknownOutputPassingOption.Allowed,
        FirstPlayExpiration = TimeSpan.FromSeconds(20.0),
    }
};
```

## <a id="schema"></a><span data-ttu-id="c0864-141">PlayReady license template XML schema</span><span class="sxs-lookup"><span data-stu-id="c0864-141">PlayReady license template XML schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>


## <a name="next-steps"></a><span data-ttu-id="c0864-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0864-142">Next steps</span></span>

<span data-ttu-id="c0864-143">Check out how to [protect with DRM](protect-with-drm.md)</span><span class="sxs-lookup"><span data-stu-id="c0864-143">Check out how to [protect with DRM](protect-with-drm.md)</span></span>