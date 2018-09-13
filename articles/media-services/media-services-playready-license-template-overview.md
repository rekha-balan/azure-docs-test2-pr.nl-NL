---
title: Media Services PlayReady license template overview
description: This topic gives an overview of a PlayReady license template that used to configure PlayReady licenses.
author: juliako
manager: erikre
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: ea0b54a1041c0008071a9b11afc81e1b91f3e409
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553078"
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="86a2c-103">Media Services PlayReady license template overview</span><span class="sxs-lookup"><span data-stu-id="86a2c-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="86a2c-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span><span class="sxs-lookup"><span data-stu-id="86a2c-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="86a2c-105">When the end user player (for example, Silverlight) tries to play your PlayReady protected content, a request is sent to the license delivery service to obtain a license.</span><span class="sxs-lookup"><span data-stu-id="86a2c-105">When the end user player (for example, Silverlight) tries to play your PlayReady protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="86a2c-106">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span><span class="sxs-lookup"><span data-stu-id="86a2c-106">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="86a2c-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span><span class="sxs-lookup"><span data-stu-id="86a2c-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="86a2c-108">Licenses contain the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to playback protected content.</span><span class="sxs-lookup"><span data-stu-id="86a2c-108">Licenses contain the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to playback protected content.</span></span>
<span data-ttu-id="86a2c-109">Below are some examples of PlayReady license restrictions that you can specify:</span><span class="sxs-lookup"><span data-stu-id="86a2c-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="86a2c-110">The DateTime from which the license is valid.</span><span class="sxs-lookup"><span data-stu-id="86a2c-110">The DateTime from which the license is valid.</span></span>
* <span data-ttu-id="86a2c-111">The DateTime value when the license expires.</span><span class="sxs-lookup"><span data-stu-id="86a2c-111">The DateTime value when the license expires.</span></span> 
* <span data-ttu-id="86a2c-112">For the license to be saved in persistent storage on the client.</span><span class="sxs-lookup"><span data-stu-id="86a2c-112">For the license to be saved in persistent storage on the client.</span></span> <span data-ttu-id="86a2c-113">Persistent licenses are typically used to allow offline playback of the content.</span><span class="sxs-lookup"><span data-stu-id="86a2c-113">Persistent licenses are typically used to allow offline playback of the content.</span></span>
* <span data-ttu-id="86a2c-114">The minimum security level that a player must have to play your content.</span><span class="sxs-lookup"><span data-stu-id="86a2c-114">The minimum security level that a player must have to play your content.</span></span> 
* <span data-ttu-id="86a2c-115">The output protection level for the output controls for audio\video content.</span><span class="sxs-lookup"><span data-stu-id="86a2c-115">The output protection level for the output controls for audio\video content.</span></span> 
* <span data-ttu-id="86a2c-116">For more information, see the Output Controls section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span><span class="sxs-lookup"><span data-stu-id="86a2c-116">For more information, see the Output Controls section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="86a2c-117">Currently, you can only configure the PlayRight of the PlayReady license (this right is required).</span><span class="sxs-lookup"><span data-stu-id="86a2c-117">Currently, you can only configure the PlayRight of the PlayReady license (this right is required).</span></span> <span data-ttu-id="86a2c-118">The PlayRight gives the client the ability to playback the content.</span><span class="sxs-lookup"><span data-stu-id="86a2c-118">The PlayRight gives the client the ability to playback the content.</span></span> <span data-ttu-id="86a2c-119">The PlayRight also allows configuring restrictions specific to playback.</span><span class="sxs-lookup"><span data-stu-id="86a2c-119">The PlayRight also allows configuring restrictions specific to playback.</span></span> <span data-ttu-id="86a2c-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="86a2c-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="86a2c-121">To configure PlayReady licenses using Media Services, you must configure the Media Services PlayReady license template.</span><span class="sxs-lookup"><span data-stu-id="86a2c-121">To configure PlayReady licenses using Media Services, you must configure the Media Services PlayReady license template.</span></span> <span data-ttu-id="86a2c-122">The template is defined in XML.</span><span class="sxs-lookup"><span data-stu-id="86a2c-122">The template is defined in XML.</span></span>

<span data-ttu-id="86a2c-123">The following example shows the simplest (and most common) template that configures a basic streaming license.</span><span class="sxs-lookup"><span data-stu-id="86a2c-123">The following example shows the simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="86a2c-124">With this license, your clients would be able to playback your PlayReady protected content.</span><span class="sxs-lookup"><span data-stu-id="86a2c-124">With this license, your clients would be able to playback your PlayReady protected content.</span></span>

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

<span data-ttu-id="86a2c-125">The XML conforms to the PlayReady license template XML schema defined in the PlayReady license template XML schema section.</span><span class="sxs-lookup"><span data-stu-id="86a2c-125">The XML conforms to the PlayReady license template XML schema defined in the PlayReady license template XML schema section.</span></span>

<span data-ttu-id="86a2c-126">Media Services also defines a set of .NET classes that could be used to serialized and deserialized to and from the XML.</span><span class="sxs-lookup"><span data-stu-id="86a2c-126">Media Services also defines a set of .NET classes that could be used to serialized and deserialized to and from the XML.</span></span> <span data-ttu-id="86a2c-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="86a2c-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="86a2c-128">that are used to configure license templates.</span><span class="sxs-lookup"><span data-stu-id="86a2c-128">that are used to configure license templates.</span></span>

<span data-ttu-id="86a2c-129">For an end-to-end example that uses .NET classes to configure the PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="86a2c-129">For an end-to-end example that uses .NET classes to configure the PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <a id="classes"></a><span data-ttu-id="86a2c-130">Media Services .NET classes that are used to configure license templates</span><span class="sxs-lookup"><span data-stu-id="86a2c-130">Media Services .NET classes that are used to configure license templates</span></span>
<span data-ttu-id="86a2c-131">The following are the main .NET classes are used to configure Media Services PlayReady license templates.</span><span class="sxs-lookup"><span data-stu-id="86a2c-131">The following are the main .NET classes are used to configure Media Services PlayReady license templates.</span></span> <span data-ttu-id="86a2c-132">These classes map to the types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="86a2c-132">These classes map to the types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="86a2c-133">The [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used to serialize and deserialize to and from the Media Services license template XML.</span><span class="sxs-lookup"><span data-stu-id="86a2c-133">The [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used to serialize and deserialize to and from the Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="86a2c-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="86a2c-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="86a2c-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents the template for the response sent back to the end user.</span><span class="sxs-lookup"><span data-stu-id="86a2c-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents the template for the response sent back to the end user.</span></span> <span data-ttu-id="86a2c-136">It contains a field for a custom data string between the license server and the application (may be useful for custom app logic) as well as a list of one or more license templates.</span><span class="sxs-lookup"><span data-stu-id="86a2c-136">It contains a field for a custom data string between the license server and the application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="86a2c-137">This is the “top level” class in the template hierarchy.</span><span class="sxs-lookup"><span data-stu-id="86a2c-137">This is the “top level” class in the template hierarchy.</span></span> <span data-ttu-id="86a2c-138">Meaning that the response template includes a list of license templates and the license templates include (directly or indirectly) all of the other classes that make up the template data to be serialized.</span><span class="sxs-lookup"><span data-stu-id="86a2c-138">Meaning that the response template includes a list of license templates and the license templates include (directly or indirectly) all of the other classes that make up the template data to be serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="86a2c-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="86a2c-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="86a2c-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - The class represents a license template for creating PlayReady licenses to be returned to the end users.</span><span class="sxs-lookup"><span data-stu-id="86a2c-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - The class represents a license template for creating PlayReady licenses to be returned to the end users.</span></span> <span data-ttu-id="86a2c-141">It contains the data on the content key in the license and any rights or restrictions to be enforced by the PlayReady DRM runtime when using the content key.</span><span class="sxs-lookup"><span data-stu-id="86a2c-141">It contains the data on the content key in the license and any rights or restrictions to be enforced by the PlayReady DRM runtime when using the content key.</span></span>

### <a id="PlayReadyPlayRight"></a><span data-ttu-id="86a2c-142">PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="86a2c-142">PlayReadyPlayRight</span></span>
<span data-ttu-id="86a2c-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents the PlayRight of a PlayReady license.</span><span class="sxs-lookup"><span data-stu-id="86a2c-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents the PlayRight of a PlayReady license.</span></span> <span data-ttu-id="86a2c-144">It grants the user the ability to playback the content subject to the zero or more restrictions configured in the license and on the PlayRight itself (for playback specific policy).</span><span class="sxs-lookup"><span data-stu-id="86a2c-144">It grants the user the ability to playback the content subject to the zero or more restrictions configured in the license and on the PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="86a2c-145">Much of the policy on the PlayRight has to do with output restrictions which control the types of outputs that the content can be played over and any restrictions that must be put in place when using a given output.</span><span class="sxs-lookup"><span data-stu-id="86a2c-145">Much of the policy on the PlayRight has to do with output restrictions which control the types of outputs that the content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="86a2c-146">For example, if the DigitalVideoOnlyContentRestriction is enabled, then the DRM runtime will only allow the video to be displayed over digital outputs (analog video outputs won’t be allowed to pass the content).</span><span class="sxs-lookup"><span data-stu-id="86a2c-146">For example, if the DigitalVideoOnlyContentRestriction is enabled, then the DRM runtime will only allow the video to be displayed over digital outputs (analog video outputs won’t be allowed to pass the content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86a2c-147">These types of restrictions can be very powerful but can also affect the consumer experience.</span><span class="sxs-lookup"><span data-stu-id="86a2c-147">These types of restrictions can be very powerful but can also affect the consumer experience.</span></span> <span data-ttu-id="86a2c-148">If the output protections are configured too restrictive, the content might be unplayable on some clients.</span><span class="sxs-lookup"><span data-stu-id="86a2c-148">If the output protections are configured too restrictive, the content might be unplayable on some clients.</span></span> <span data-ttu-id="86a2c-149">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span><span class="sxs-lookup"><span data-stu-id="86a2c-149">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="86a2c-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="86a2c-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <a id="schema"></a><span data-ttu-id="86a2c-151">PlayReady license template XML schema</span><span class="sxs-lookup"><span data-stu-id="86a2c-151">PlayReady license template XML schema</span></span>
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="86a2c-152">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="86a2c-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="86a2c-153">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="86a2c-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

