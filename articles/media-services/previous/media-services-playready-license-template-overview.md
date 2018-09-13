---
title: Media Services PlayReady license template overview
description: This topic gives an overview of a PlayReady license template that is used to configure PlayReady licenses.
author: juliako
manager: cfowler
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 74a2eb579f38cfc885234fac7fd3ad4be1747ad7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856446"
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="c9619-103">Media Services PlayReady license template overview</span><span class="sxs-lookup"><span data-stu-id="c9619-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="c9619-104">Azure Media Services now provides a service for delivering PlayReady licenses.</span><span class="sxs-lookup"><span data-stu-id="c9619-104">Azure Media Services now provides a service for delivering PlayReady licenses.</span></span> <span data-ttu-id="c9619-105">When the player (for example, Silverlight) tries to play your PlayReady-protected content, a request is sent to the license delivery service to obtain a license.</span><span class="sxs-lookup"><span data-stu-id="c9619-105">When the player (for example, Silverlight) tries to play your PlayReady-protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="c9619-106">If the license service approves the request, it issues the license that is sent to the client and is used to decrypt and play the specified content.</span><span class="sxs-lookup"><span data-stu-id="c9619-106">If the license service approves the request, it issues the license that is sent to the client and is used to decrypt and play the specified content.</span></span>

<span data-ttu-id="c9619-107">Media Services also provides APIs that you can use to configure your PlayReady licenses.</span><span class="sxs-lookup"><span data-stu-id="c9619-107">Media Services also provides APIs that you can use to configure your PlayReady licenses.</span></span> <span data-ttu-id="c9619-108">Licenses contain the rights and restrictions that you want the PlayReady digital rights management (DRM) runtime to enforce when a user tries to play back protected content.</span><span class="sxs-lookup"><span data-stu-id="c9619-108">Licenses contain the rights and restrictions that you want the PlayReady digital rights management (DRM) runtime to enforce when a user tries to play back protected content.</span></span>
<span data-ttu-id="c9619-109">Here are some examples of PlayReady license restrictions that you can specify:</span><span class="sxs-lookup"><span data-stu-id="c9619-109">Here are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="c9619-110">The date and time from which the license is valid.</span><span class="sxs-lookup"><span data-stu-id="c9619-110">The date and time from which the license is valid.</span></span>
* <span data-ttu-id="c9619-111">The DateTime value when the license expires.</span><span class="sxs-lookup"><span data-stu-id="c9619-111">The DateTime value when the license expires.</span></span> 
* <span data-ttu-id="c9619-112">For the license to be saved in persistent storage on the client.</span><span class="sxs-lookup"><span data-stu-id="c9619-112">For the license to be saved in persistent storage on the client.</span></span> <span data-ttu-id="c9619-113">Persistent licenses are typically used to allow offline playback of the content.</span><span class="sxs-lookup"><span data-stu-id="c9619-113">Persistent licenses are typically used to allow offline playback of the content.</span></span>
* <span data-ttu-id="c9619-114">The minimum security level that a player must have to play your content.</span><span class="sxs-lookup"><span data-stu-id="c9619-114">The minimum security level that a player must have to play your content.</span></span> 
* <span data-ttu-id="c9619-115">The output protection level for the output controls for audio\video content.</span><span class="sxs-lookup"><span data-stu-id="c9619-115">The output protection level for the output controls for audio\video content.</span></span> 
* <span data-ttu-id="c9619-116">For more information, see the "Output Controls" section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span><span class="sxs-lookup"><span data-stu-id="c9619-116">For more information, see the "Output Controls" section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="c9619-117">Currently, you can only configure the PlayRight of the PlayReady license.</span><span class="sxs-lookup"><span data-stu-id="c9619-117">Currently, you can only configure the PlayRight of the PlayReady license.</span></span> <span data-ttu-id="c9619-118">This right is required.</span><span class="sxs-lookup"><span data-stu-id="c9619-118">This right is required.</span></span> <span data-ttu-id="c9619-119">The PlayRight gives the client the ability to play back the content.</span><span class="sxs-lookup"><span data-stu-id="c9619-119">The PlayRight gives the client the ability to play back the content.</span></span> <span data-ttu-id="c9619-120">You also can use the PlayRight to configure restrictions specific to playback.</span><span class="sxs-lookup"><span data-stu-id="c9619-120">You also can use the PlayRight to configure restrictions specific to playback.</span></span> <span data-ttu-id="c9619-121">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="c9619-121">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="c9619-122">To configure PlayReady licenses by using Media Services, you must configure the Media Services PlayReady license template.</span><span class="sxs-lookup"><span data-stu-id="c9619-122">To configure PlayReady licenses by using Media Services, you must configure the Media Services PlayReady license template.</span></span> <span data-ttu-id="c9619-123">The template is defined in XML.</span><span class="sxs-lookup"><span data-stu-id="c9619-123">The template is defined in XML.</span></span>

<span data-ttu-id="c9619-124">The following example shows the simplest (and most common) template that configures a basic streaming license.</span><span class="sxs-lookup"><span data-stu-id="c9619-124">The following example shows the simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="c9619-125">With this license, your clients can play back your PlayReady-protected content.</span><span class="sxs-lookup"><span data-stu-id="c9619-125">With this license, your clients can play back your PlayReady-protected content.</span></span>

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

<span data-ttu-id="c9619-126">The XML conforms to the PlayReady license template XML schema defined in the "PlayReady license template XML schema" section.</span><span class="sxs-lookup"><span data-stu-id="c9619-126">The XML conforms to the PlayReady license template XML schema defined in the "PlayReady license template XML schema" section.</span></span>

<span data-ttu-id="c9619-127">Media Services also defines a set of .NET classes that can be used to serialize and deserialize to and from the XML.</span><span class="sxs-lookup"><span data-stu-id="c9619-127">Media Services also defines a set of .NET classes that can be used to serialize and deserialize to and from the XML.</span></span> <span data-ttu-id="c9619-128">For a description of the main classes, see the [Media Services .NET classes](media-services-playready-license-template-overview.md#classes) that are used to configure license templates.</span><span class="sxs-lookup"><span data-stu-id="c9619-128">For a description of the main classes, see the [Media Services .NET classes](media-services-playready-license-template-overview.md#classes) that are used to configure license templates.</span></span>

<span data-ttu-id="c9619-129">For an end-to-end example that uses .NET classes to configure the PlayReady license template, see [Use PlayReady dynamic encryption and the license delivery service](media-services-protect-with-playready-widevine.md).</span><span class="sxs-lookup"><span data-stu-id="c9619-129">For an end-to-end example that uses .NET classes to configure the PlayReady license template, see [Use PlayReady dynamic encryption and the license delivery service](media-services-protect-with-playready-widevine.md).</span></span>

## <a id="classes"></a><span data-ttu-id="c9619-130">Media Services .NET classes that are used to configure license templates</span><span class="sxs-lookup"><span data-stu-id="c9619-130">Media Services .NET classes that are used to configure license templates</span></span>
<span data-ttu-id="c9619-131">The following classes are the main .NET classes that are used to configure Media Services PlayReady license templates.</span><span class="sxs-lookup"><span data-stu-id="c9619-131">The following classes are the main .NET classes that are used to configure Media Services PlayReady license templates.</span></span> <span data-ttu-id="c9619-132">These classes map to the types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="c9619-132">These classes map to the types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="c9619-133">The [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used to serialize and deserialize to and from the Media Services license template XML.</span><span class="sxs-lookup"><span data-stu-id="c9619-133">The [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used to serialize and deserialize to and from the Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="c9619-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="c9619-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="c9619-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx): This class represents the template for the response sent back to the user.</span><span class="sxs-lookup"><span data-stu-id="c9619-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx): This class represents the template for the response sent back to the user.</span></span> <span data-ttu-id="c9619-136">It contains a field for a custom data string between the license server and the application (which might be useful for custom app logic).</span><span class="sxs-lookup"><span data-stu-id="c9619-136">It contains a field for a custom data string between the license server and the application (which might be useful for custom app logic).</span></span> <span data-ttu-id="c9619-137">It also contains a list of one or more license templates.</span><span class="sxs-lookup"><span data-stu-id="c9619-137">It also contains a list of one or more license templates.</span></span>

<span data-ttu-id="c9619-138">As the "top-level" class in the template hierarchy, the response template includes a list of license templates.</span><span class="sxs-lookup"><span data-stu-id="c9619-138">As the "top-level" class in the template hierarchy, the response template includes a list of license templates.</span></span> <span data-ttu-id="c9619-139">The license templates include (directly or indirectly) all the other classes that make up the template data to be serialized.</span><span class="sxs-lookup"><span data-stu-id="c9619-139">The license templates include (directly or indirectly) all the other classes that make up the template data to be serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="c9619-140">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="c9619-140">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="c9619-141">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx): This class represents a license template that is used to create PlayReady licenses to be returned to users.</span><span class="sxs-lookup"><span data-stu-id="c9619-141">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx): This class represents a license template that is used to create PlayReady licenses to be returned to users.</span></span> <span data-ttu-id="c9619-142">It contains the data on the content key in the license.</span><span class="sxs-lookup"><span data-stu-id="c9619-142">It contains the data on the content key in the license.</span></span> <span data-ttu-id="c9619-143">It also includes any rights or restrictions that the PlayReady DRM runtime must enforce when the content key is used.</span><span class="sxs-lookup"><span data-stu-id="c9619-143">It also includes any rights or restrictions that the PlayReady DRM runtime must enforce when the content key is used.</span></span>

### <a id="PlayReadyPlayRight"></a><span data-ttu-id="c9619-144">PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="c9619-144">PlayReadyPlayRight</span></span>
<span data-ttu-id="c9619-145">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx): This class represents the PlayRight of a PlayReady license.</span><span class="sxs-lookup"><span data-stu-id="c9619-145">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx): This class represents the PlayRight of a PlayReady license.</span></span> <span data-ttu-id="c9619-146">It grants the user the ability to play back the content subject to any restrictions configured in the license and on the PlayRight itself (for playback-specific policy).</span><span class="sxs-lookup"><span data-stu-id="c9619-146">It grants the user the ability to play back the content subject to any restrictions configured in the license and on the PlayRight itself (for playback-specific policy).</span></span> <span data-ttu-id="c9619-147">Much of the policy on a PlayRight concerns output restrictions that control the types of outputs that the content can be played over.</span><span class="sxs-lookup"><span data-stu-id="c9619-147">Much of the policy on a PlayRight concerns output restrictions that control the types of outputs that the content can be played over.</span></span> <span data-ttu-id="c9619-148">It also includes any restrictions that must be put in place when a given output is used.</span><span class="sxs-lookup"><span data-stu-id="c9619-148">It also includes any restrictions that must be put in place when a given output is used.</span></span> <span data-ttu-id="c9619-149">For example, if DigitalVideoOnlyContentRestriction is enabled, the DRM runtime only allows the video to be displayed over digital outputs.</span><span class="sxs-lookup"><span data-stu-id="c9619-149">For example, if DigitalVideoOnlyContentRestriction is enabled, the DRM runtime only allows the video to be displayed over digital outputs.</span></span> <span data-ttu-id="c9619-150">(Analog video outputs aren't allowed to pass the content.)</span><span class="sxs-lookup"><span data-stu-id="c9619-150">(Analog video outputs aren't allowed to pass the content.)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9619-151">These types of restrictions can be powerful, but they also can affect the consumer experience.</span><span class="sxs-lookup"><span data-stu-id="c9619-151">These types of restrictions can be powerful, but they also can affect the consumer experience.</span></span> <span data-ttu-id="c9619-152">If the output protections are too restrictive, the content might be unplayable on some clients.</span><span class="sxs-lookup"><span data-stu-id="c9619-152">If the output protections are too restrictive, the content might be unplayable on some clients.</span></span> <span data-ttu-id="c9619-153">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/).</span><span class="sxs-lookup"><span data-stu-id="c9619-153">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/).</span></span>
> 
> 

<span data-ttu-id="c9619-154">For an example of the protection levels that Silverlight supports, see [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="c9619-154">For an example of the protection levels that Silverlight supports, see [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <a id="schema"></a><span data-ttu-id="c9619-155">PlayReady license template XML schema</span><span class="sxs-lookup"><span data-stu-id="c9619-155">PlayReady license template XML schema</span></span>
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="c9619-156">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="c9619-156">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c9619-157">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="c9619-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

