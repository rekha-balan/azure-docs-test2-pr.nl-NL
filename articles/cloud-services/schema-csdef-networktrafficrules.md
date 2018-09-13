---
title: Azure Cloud Services Def. NetworkTrafficRules Schema | Microsoft Docs
ms.custom: ''
ms.date: 04/14/2015
services: cloud-services
ms.reviewer: ''
ms.service: cloud-services
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 351b369f-365e-46c1-82ce-03fc3655cc88
caps.latest.revision: 17
author: jpconnock
ms.author: jeconnoc
manager: timlt
ms.openlocfilehash: 71c791c9ac6f679f0f67b014c8fb5dd915d1a3e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869786"
---
# <a name="azure-cloud-services-definition-networktrafficrules-schema"></a><span data-ttu-id="c1f69-102">Azure Cloud Services Definition NetworkTrafficRules Schema</span><span class="sxs-lookup"><span data-stu-id="c1f69-102">Azure Cloud Services Definition NetworkTrafficRules Schema</span></span>
<span data-ttu-id="c1f69-103">The `NetworkTrafficRules` node is an optional element in the service definition file that specifies how roles communicate with each other.</span><span class="sxs-lookup"><span data-stu-id="c1f69-103">The `NetworkTrafficRules` node is an optional element in the service definition file that specifies how roles communicate with each other.</span></span> <span data-ttu-id="c1f69-104">It limits which roles can access the internal endpoints of the specific role.</span><span class="sxs-lookup"><span data-stu-id="c1f69-104">It limits which roles can access the internal endpoints of the specific role.</span></span> <span data-ttu-id="c1f69-105">The `NetworkTrafficRules` is not a standalone element; it is combined with two or more roles in a service definition file.</span><span class="sxs-lookup"><span data-stu-id="c1f69-105">The `NetworkTrafficRules` is not a standalone element; it is combined with two or more roles in a service definition file.</span></span>

<span data-ttu-id="c1f69-106">The default extension for the service definition file is .csdef.</span><span class="sxs-lookup"><span data-stu-id="c1f69-106">The default extension for the service definition file is .csdef.</span></span>

> [!NOTE]
>  <span data-ttu-id="c1f69-107">The `NetworkTrafficRules` node is only available using the Azure SDK version 1.3 or higher.</span><span class="sxs-lookup"><span data-stu-id="c1f69-107">The `NetworkTrafficRules` node is only available using the Azure SDK version 1.3 or higher.</span></span>

## <a name="basic-service-definition-schema-for-the-network-traffic-rules"></a><span data-ttu-id="c1f69-108">Basic service definition schema for the network traffic rules</span><span class="sxs-lookup"><span data-stu-id="c1f69-108">Basic service definition schema for the network traffic rules</span></span>
<span data-ttu-id="c1f69-109">The basic format of a service definition file containing network traffic definitions is as follows.</span><span class="sxs-lookup"><span data-stu-id="c1f69-109">The basic format of a service definition file containing network traffic definitions is as follows.</span></span>

```xml
<ServiceDefinition …>
   <NetworkTrafficRules>
      <OnlyAllowTrafficTo>
         <Destinations>
            <RoleEndpoint endpointName="<name-of-the-endpoint>" roleName="<name-of-the-role-containing-the-endpoint>"/>
         </Destinations>
         <AllowAllTraffic/>
         <WhenSource matches="[AnyRule]">
            <FromRole roleName="<name-of-the-role-to-allow-traffic-from>"/>
         </WhenSource>
      </OnlyAllowTrafficTo>
   </NetworkTrafficRules>
</ServiceDefinition>
```

## <a name="schema-elements"></a><span data-ttu-id="c1f69-110">Schema Elements</span><span class="sxs-lookup"><span data-stu-id="c1f69-110">Schema Elements</span></span>
<span data-ttu-id="c1f69-111">The `NetworkTrafficRules` node of the service definition file includes these elements, described in detail in subsequent sections in this topic:</span><span class="sxs-lookup"><span data-stu-id="c1f69-111">The `NetworkTrafficRules` node of the service definition file includes these elements, described in detail in subsequent sections in this topic:</span></span>

[<span data-ttu-id="c1f69-112">NetworkTrafficRules Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-112">NetworkTrafficRules Element</span></span>](#NetworkTrafficRules)

[<span data-ttu-id="c1f69-113">OnlyAllowTrafficTo Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-113">OnlyAllowTrafficTo Element</span></span>](#OnlyAllowTrafficTo)

[<span data-ttu-id="c1f69-114">Destinations Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-114">Destinations Element</span></span>](#Destinations)

[<span data-ttu-id="c1f69-115">RoleEndpoint Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-115">RoleEndpoint Element</span></span>](#RoleEndpoint)

[<span data-ttu-id="c1f69-116">AllowAllTraffic Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-116">AllowAllTraffic Element</span></span>](#AllowAllTraffic)

[<span data-ttu-id="c1f69-117">WhenSource Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-117">WhenSource Element</span></span>](#WhenSource)

[<span data-ttu-id="c1f69-118">FromRole Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-118">FromRole Element</span></span>](#FromRole)

##  <a name="NetworkTrafficRules"></a> <span data-ttu-id="c1f69-119">NetworkTrafficRules Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-119">NetworkTrafficRules Element</span></span>
<span data-ttu-id="c1f69-120">The `NetworkTrafficRules` element specifies which roles can communicate with which endpoint on another role.</span><span class="sxs-lookup"><span data-stu-id="c1f69-120">The `NetworkTrafficRules` element specifies which roles can communicate with which endpoint on another role.</span></span> <span data-ttu-id="c1f69-121">A service can contain one `NetworkTrafficRules` definition.</span><span class="sxs-lookup"><span data-stu-id="c1f69-121">A service can contain one `NetworkTrafficRules` definition.</span></span>

##  <a name="OnlyAllowTrafficTo"></a> <span data-ttu-id="c1f69-122">OnlyAllowTrafficTo Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-122">OnlyAllowTrafficTo Element</span></span>
<span data-ttu-id="c1f69-123">The `OnlyAllowTrafficTo` element describes a collection of destination endpoints and the roles that can communicate with them.</span><span class="sxs-lookup"><span data-stu-id="c1f69-123">The `OnlyAllowTrafficTo` element describes a collection of destination endpoints and the roles that can communicate with them.</span></span> <span data-ttu-id="c1f69-124">You can specify multiple `OnlyAllowTrafficTo` nodes.</span><span class="sxs-lookup"><span data-stu-id="c1f69-124">You can specify multiple `OnlyAllowTrafficTo` nodes.</span></span>

##  <a name="Destinations"></a> <span data-ttu-id="c1f69-125">Destinations Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-125">Destinations Element</span></span>
<span data-ttu-id="c1f69-126">The `Destinations` element describes a collection of RoleEndpoints than can be communicated with.</span><span class="sxs-lookup"><span data-stu-id="c1f69-126">The `Destinations` element describes a collection of RoleEndpoints than can be communicated with.</span></span>

##  <a name="RoleEndpoint"></a> <span data-ttu-id="c1f69-127">RoleEndpoint Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-127">RoleEndpoint Element</span></span>
<span data-ttu-id="c1f69-128">The `RoleEndpoint` element describes an endpoint on a role to allow communications with.</span><span class="sxs-lookup"><span data-stu-id="c1f69-128">The `RoleEndpoint` element describes an endpoint on a role to allow communications with.</span></span> <span data-ttu-id="c1f69-129">You can specify multiple `RoleEndpoint` elements if there are more than one endpoint on the role.</span><span class="sxs-lookup"><span data-stu-id="c1f69-129">You can specify multiple `RoleEndpoint` elements if there are more than one endpoint on the role.</span></span>

| <span data-ttu-id="c1f69-130">Attribute</span><span class="sxs-lookup"><span data-stu-id="c1f69-130">Attribute</span></span>      | <span data-ttu-id="c1f69-131">Type</span><span class="sxs-lookup"><span data-stu-id="c1f69-131">Type</span></span>     | <span data-ttu-id="c1f69-132">Description</span><span class="sxs-lookup"><span data-stu-id="c1f69-132">Description</span></span> |
| -------------- | -------- | ----------- |
| `endpointName` | `string` | <span data-ttu-id="c1f69-133">Required.</span><span class="sxs-lookup"><span data-stu-id="c1f69-133">Required.</span></span> <span data-ttu-id="c1f69-134">The name of the endpoint to allow traffic to.</span><span class="sxs-lookup"><span data-stu-id="c1f69-134">The name of the endpoint to allow traffic to.</span></span>|
| `roleName`     | `string` | <span data-ttu-id="c1f69-135">Required.</span><span class="sxs-lookup"><span data-stu-id="c1f69-135">Required.</span></span> <span data-ttu-id="c1f69-136">The name of the web role to allow communication to.</span><span class="sxs-lookup"><span data-stu-id="c1f69-136">The name of the web role to allow communication to.</span></span>|

## <a name="allowalltraffic-element"></a><span data-ttu-id="c1f69-137">AllowAllTraffic Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-137">AllowAllTraffic Element</span></span>
<span data-ttu-id="c1f69-138">The `AllowAllTraffic` element is a rule that allows all roles to communicate with the endpoints defined in the `Destinations` node.</span><span class="sxs-lookup"><span data-stu-id="c1f69-138">The `AllowAllTraffic` element is a rule that allows all roles to communicate with the endpoints defined in the `Destinations` node.</span></span>

##  <a name="WhenSource"></a> <span data-ttu-id="c1f69-139">WhenSource Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-139">WhenSource Element</span></span>
<span data-ttu-id="c1f69-140">The `WhenSource` element describes a collection of roles than can communicate with the endpoints defined in the `Destinations` node.</span><span class="sxs-lookup"><span data-stu-id="c1f69-140">The `WhenSource` element describes a collection of roles than can communicate with the endpoints defined in the `Destinations` node.</span></span>

| <span data-ttu-id="c1f69-141">Attribute</span><span class="sxs-lookup"><span data-stu-id="c1f69-141">Attribute</span></span> | <span data-ttu-id="c1f69-142">Type</span><span class="sxs-lookup"><span data-stu-id="c1f69-142">Type</span></span>     | <span data-ttu-id="c1f69-143">Description</span><span class="sxs-lookup"><span data-stu-id="c1f69-143">Description</span></span> |
| --------- | -------- | ----------- |
| `matches` | `string` | <span data-ttu-id="c1f69-144">Required.</span><span class="sxs-lookup"><span data-stu-id="c1f69-144">Required.</span></span> <span data-ttu-id="c1f69-145">Specifies the rule to apply when allowing communications.</span><span class="sxs-lookup"><span data-stu-id="c1f69-145">Specifies the rule to apply when allowing communications.</span></span> <span data-ttu-id="c1f69-146">The only valid value is currently `AnyRule`.</span><span class="sxs-lookup"><span data-stu-id="c1f69-146">The only valid value is currently `AnyRule`.</span></span>|
  
##  <a name="FromRole"></a> <span data-ttu-id="c1f69-147">FromRole Element</span><span class="sxs-lookup"><span data-stu-id="c1f69-147">FromRole Element</span></span>
<span data-ttu-id="c1f69-148">The `FromRole` element specifies the roles that can communicate with the endpoints defined in the `Destinations` node.</span><span class="sxs-lookup"><span data-stu-id="c1f69-148">The `FromRole` element specifies the roles that can communicate with the endpoints defined in the `Destinations` node.</span></span> <span data-ttu-id="c1f69-149">You can specify multiple `FromRole` elements if there are more than one role that can communicate with the endpoints.</span><span class="sxs-lookup"><span data-stu-id="c1f69-149">You can specify multiple `FromRole` elements if there are more than one role that can communicate with the endpoints.</span></span>

| <span data-ttu-id="c1f69-150">Attribute</span><span class="sxs-lookup"><span data-stu-id="c1f69-150">Attribute</span></span>  | <span data-ttu-id="c1f69-151">Type</span><span class="sxs-lookup"><span data-stu-id="c1f69-151">Type</span></span>     | <span data-ttu-id="c1f69-152">Description</span><span class="sxs-lookup"><span data-stu-id="c1f69-152">Description</span></span> |
| ---------- | -------- | ----------- |
| `roleName` | `string` | <span data-ttu-id="c1f69-153">Required.</span><span class="sxs-lookup"><span data-stu-id="c1f69-153">Required.</span></span> <span data-ttu-id="c1f69-154">The name for role from which to allow communication.</span><span class="sxs-lookup"><span data-stu-id="c1f69-154">The name for role from which to allow communication.</span></span>|

## <a name="see-also"></a><span data-ttu-id="c1f69-155">See Also</span><span class="sxs-lookup"><span data-stu-id="c1f69-155">See Also</span></span>
[<span data-ttu-id="c1f69-156">Cloud Service (classic) Definition Schema</span><span class="sxs-lookup"><span data-stu-id="c1f69-156">Cloud Service (classic) Definition Schema</span></span>](schema-csdef-file.md)