---
title: Interpret the Azure Active Directory audit log schema in Azure Monitor (preview) | Microsoft Docs
description: Describe the Azure AD audit log schema for use in Azure Monitor (preview)
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 07/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 8cbeeabfe254e40343632e9d6db3a55c3ea78bbb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857828"
---
# <a name="interpret-the-azure-ad-audit-logs-schema-in-azure-monitor-preview"></a><span data-ttu-id="98a93-103">Interpret the Azure AD audit logs schema in Azure Monitor (preview)</span><span class="sxs-lookup"><span data-stu-id="98a93-103">Interpret the Azure AD audit logs schema in Azure Monitor (preview)</span></span>

<span data-ttu-id="98a93-104">This article describes the Azure Active Directory (Azure AD) audit log schema in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="98a93-104">This article describes the Azure Active Directory (Azure AD) audit log schema in Azure Monitor.</span></span> <span data-ttu-id="98a93-105">Each individual log entry is stored as text and formatted as a JSON blob, as shown in the following two examples:</span><span class="sxs-lookup"><span data-stu-id="98a93-105">Each individual log entry is stored as text and formatted as a JSON blob, as shown in the following two examples:</span></span> 

```json
{ 
    "records": [ 
    { 
        "time": "2018-03-17T00:14:31.2585575Z", 
        "operationName": "Change password (self-service)",
        "operationVersion": "1.0",
        "category": "Audit", 
        "tenantId": "bf85dc9d-cb43-44a4-80c4-469e8c58249e", 
        "resultType": "Success", 
        "resultSignature": "-1", 
        "resultDescription": "None", 
        "durationMs": "-1", 
        "correlationId": "60d5e89a-b890-413f-9e25-a047734afe9f", 
        "identity": "sreens@wingtiptoysonline.com", 
        "Level": "Informational", 
        "location": "WUS", 
        "properties": { 
            "identityType": "UPN", 
            "operationType": "Update", 
            "additionalDetails": "None", 
            "additionalTargets": "", 
            "targetUpdatedProperties": "", 
            "targetResourceType": "UPN__TenantContextID__PUID__ObjectID__ObjectClass", 
            "targetResourceName": "sreens@wingtiptoysonline.com__bf85dc9d-cb43-44a4-80c4-469e8c58249e__1003BFFD9FEB17DB__7a408bdd-7d97-4574-8511-dd747b56465d__User", 
            "auditEventCategory": "UserManagement" 
        } 
    } 
    ] 
} 
```

```json
{ 
    "records": [ 
    { 
        "time": "2018-03-18T19:47:43.0368859Z", 
        "operationName": "Update service principal.", 
        "operationVersion": "1.0", 
        "category": "Audit", 
        "tenantId": "bf85dc9d-cb43-44a4-80c4-469e8c58249e", 
        "resultType": "Success", 
        "resultSignature": "-1", 
        "durationMs": "-1", 
        "callerIpAddress": "<null>", 
        "correlationId": "14916c7a-5a7d-44e8-9b06-74b49efb08ee", 
        "identity": "NA", 
        "Level": "Informational", 
        "properties": { 
            "identityType": "NA", 
            "operationType": "Update", 
            "additionalDetails": {}, 
            "additionalTargets": "", 
            "targetUpdatedProperties": [ 
            { 
                "Name": "Included Updated Properties", 
                "OldValue": null, 
                "NewValue": "" 
            }, 
            { 
                "Name": "TargetId.ServicePrincipalNames", 
                "OldValue": null, 
                "NewValue": "http://adapplicationregistry.onmicrosoft.com/salesforce.com/primary;cd3ed3de-93ee-400b-8b19-b61ef44a0f29" 
            } 
            ], 
        "targetResourceType": "Other__ObjectID__ObjectClass__Name__AppId__SPN", 
        "targetResourceName": "ServicePrincipal_ea70a262-4da3-440a-b396-9734ddfd9df2__ea70a262-4da3-440a-b396-9734ddfd9df2__ServicePrincipal__Salesforce__cd3ed3de-93ee-400b-8b19-b61ef44a0f29__http://adapplicationregistry.onmicrosoft.com/salesforce.com/primary;cd3ed3de-93ee-400b-8b19-b61ef44a0f29", 
        "auditEventCategory": "ApplicationManagement" 
      } 
    } 
    ] 
} 
```

## <a name="field-and-property-descriptions"></a><span data-ttu-id="98a93-106">Field and property descriptions</span><span class="sxs-lookup"><span data-stu-id="98a93-106">Field and property descriptions</span></span>

| <span data-ttu-id="98a93-107">Field name</span><span class="sxs-lookup"><span data-stu-id="98a93-107">Field name</span></span> | <span data-ttu-id="98a93-108">Description</span><span class="sxs-lookup"><span data-stu-id="98a93-108">Description</span></span> |
|------------|-------------|
| <span data-ttu-id="98a93-109">time</span><span class="sxs-lookup"><span data-stu-id="98a93-109">time</span></span>       | <span data-ttu-id="98a93-110">The date and time (UTC).</span><span class="sxs-lookup"><span data-stu-id="98a93-110">The date and time (UTC).</span></span> |
| <span data-ttu-id="98a93-111">operationName</span><span class="sxs-lookup"><span data-stu-id="98a93-111">operationName</span></span> | <span data-ttu-id="98a93-112">The name of the operation.</span><span class="sxs-lookup"><span data-stu-id="98a93-112">The name of the operation.</span></span> |
| <span data-ttu-id="98a93-113">operationVersion</span><span class="sxs-lookup"><span data-stu-id="98a93-113">operationVersion</span></span> | <span data-ttu-id="98a93-114">The REST API version that's requested by the client.</span><span class="sxs-lookup"><span data-stu-id="98a93-114">The REST API version that's requested by the client.</span></span> |
| <span data-ttu-id="98a93-115">category</span><span class="sxs-lookup"><span data-stu-id="98a93-115">category</span></span> | <span data-ttu-id="98a93-116">Currently, *Audit* is the only supported value.</span><span class="sxs-lookup"><span data-stu-id="98a93-116">Currently, *Audit* is the only supported value.</span></span> |
| <span data-ttu-id="98a93-117">tenantId</span><span class="sxs-lookup"><span data-stu-id="98a93-117">tenantId</span></span> | <span data-ttu-id="98a93-118">The tenant GUID that's associated with the logs.</span><span class="sxs-lookup"><span data-stu-id="98a93-118">The tenant GUID that's associated with the logs.</span></span> |
| <span data-ttu-id="98a93-119">resultType</span><span class="sxs-lookup"><span data-stu-id="98a93-119">resultType</span></span> | <span data-ttu-id="98a93-120">The result of the operation.</span><span class="sxs-lookup"><span data-stu-id="98a93-120">The result of the operation.</span></span> <span data-ttu-id="98a93-121">The result can be *Success* or *Failure*.</span><span class="sxs-lookup"><span data-stu-id="98a93-121">The result can be *Success* or *Failure*.</span></span> |
| <span data-ttu-id="98a93-122">resultSignature</span><span class="sxs-lookup"><span data-stu-id="98a93-122">resultSignature</span></span> |  <span data-ttu-id="98a93-123">This field is unmapped, and you can safely ignore it.</span><span class="sxs-lookup"><span data-stu-id="98a93-123">This field is unmapped, and you can safely ignore it.</span></span> | 
| <span data-ttu-id="98a93-124">resultDescription</span><span class="sxs-lookup"><span data-stu-id="98a93-124">resultDescription</span></span> | <span data-ttu-id="98a93-125">An additional description of the result, where available.</span><span class="sxs-lookup"><span data-stu-id="98a93-125">An additional description of the result, where available.</span></span> | 
| <span data-ttu-id="98a93-126">durationMs</span><span class="sxs-lookup"><span data-stu-id="98a93-126">durationMs</span></span> |  <span data-ttu-id="98a93-127">This field is unmapped, and you can safely ignore it.</span><span class="sxs-lookup"><span data-stu-id="98a93-127">This field is unmapped, and you can safely ignore it.</span></span> |
| <span data-ttu-id="98a93-128">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="98a93-128">callerIpAddress</span></span> | <span data-ttu-id="98a93-129">The IP address of the client that made the request.</span><span class="sxs-lookup"><span data-stu-id="98a93-129">The IP address of the client that made the request.</span></span> | 
| <span data-ttu-id="98a93-130">correlationId</span><span class="sxs-lookup"><span data-stu-id="98a93-130">correlationId</span></span> | <span data-ttu-id="98a93-131">An optional GUID that's passed by the client.</span><span class="sxs-lookup"><span data-stu-id="98a93-131">An optional GUID that's passed by the client.</span></span> <span data-ttu-id="98a93-132">It can help correlate client-side operations with server-side operations and it's useful when you're tracking logs that span services.</span><span class="sxs-lookup"><span data-stu-id="98a93-132">It can help correlate client-side operations with server-side operations and it's useful when you're tracking logs that span services.</span></span> |
| <span data-ttu-id="98a93-133">identity</span><span class="sxs-lookup"><span data-stu-id="98a93-133">identity</span></span> | <span data-ttu-id="98a93-134">The identity from the token that was presented when you made the request.</span><span class="sxs-lookup"><span data-stu-id="98a93-134">The identity from the token that was presented when you made the request.</span></span> <span data-ttu-id="98a93-135">The identity can be a user account, system account, or service principal.</span><span class="sxs-lookup"><span data-stu-id="98a93-135">The identity can be a user account, system account, or service principal.</span></span> |
| <span data-ttu-id="98a93-136">level</span><span class="sxs-lookup"><span data-stu-id="98a93-136">level</span></span> | <span data-ttu-id="98a93-137">The message type.</span><span class="sxs-lookup"><span data-stu-id="98a93-137">The message type.</span></span> <span data-ttu-id="98a93-138">For audit logs, the level is always *Informational*.</span><span class="sxs-lookup"><span data-stu-id="98a93-138">For audit logs, the level is always *Informational*.</span></span> |
| <span data-ttu-id="98a93-139">location</span><span class="sxs-lookup"><span data-stu-id="98a93-139">location</span></span> | <span data-ttu-id="98a93-140">The location of the datacenter.</span><span class="sxs-lookup"><span data-stu-id="98a93-140">The location of the datacenter.</span></span> |
| <span data-ttu-id="98a93-141">properties</span><span class="sxs-lookup"><span data-stu-id="98a93-141">properties</span></span> | <span data-ttu-id="98a93-142">Lists the supported properties that are related to an audit log.</span><span class="sxs-lookup"><span data-stu-id="98a93-142">Lists the supported properties that are related to an audit log.</span></span> <span data-ttu-id="98a93-143">For more information, see the next table.</span><span class="sxs-lookup"><span data-stu-id="98a93-143">For more information, see the next table.</span></span> | 

<br>

| <span data-ttu-id="98a93-144">Property name</span><span class="sxs-lookup"><span data-stu-id="98a93-144">Property name</span></span> | <span data-ttu-id="98a93-145">Description</span><span class="sxs-lookup"><span data-stu-id="98a93-145">Description</span></span> |
|---------------|-------------|
| <span data-ttu-id="98a93-146">AuditEventCategory</span><span class="sxs-lookup"><span data-stu-id="98a93-146">AuditEventCategory</span></span> | <span data-ttu-id="98a93-147">The type of audit event.</span><span class="sxs-lookup"><span data-stu-id="98a93-147">The type of audit event.</span></span> <span data-ttu-id="98a93-148">It can be *User Management*, *Application Management*, or another type.</span><span class="sxs-lookup"><span data-stu-id="98a93-148">It can be *User Management*, *Application Management*, or another type.</span></span>|
| <span data-ttu-id="98a93-149">Identity Type</span><span class="sxs-lookup"><span data-stu-id="98a93-149">Identity Type</span></span> | <span data-ttu-id="98a93-150">The type can be *Application* or *User*.</span><span class="sxs-lookup"><span data-stu-id="98a93-150">The type can be *Application* or *User*.</span></span> |
| <span data-ttu-id="98a93-151">Operation Type</span><span class="sxs-lookup"><span data-stu-id="98a93-151">Operation Type</span></span> | <span data-ttu-id="98a93-152">The type can be *Add*, *Update*, *Delete*.</span><span class="sxs-lookup"><span data-stu-id="98a93-152">The type can be *Add*, *Update*, *Delete*.</span></span> <span data-ttu-id="98a93-153">or *Other*.</span><span class="sxs-lookup"><span data-stu-id="98a93-153">or *Other*.</span></span> |
| <span data-ttu-id="98a93-154">Target Resource Type</span><span class="sxs-lookup"><span data-stu-id="98a93-154">Target Resource Type</span></span> | <span data-ttu-id="98a93-155">Specifies the target resource type that the operation was performed on.</span><span class="sxs-lookup"><span data-stu-id="98a93-155">Specifies the target resource type that the operation was performed on.</span></span> <span data-ttu-id="98a93-156">The type can be *Application*, *User*, *Role*, *Policy*</span><span class="sxs-lookup"><span data-stu-id="98a93-156">The type can be *Application*, *User*, *Role*, *Policy*</span></span> | 
| <span data-ttu-id="98a93-157">Target Resource Name</span><span class="sxs-lookup"><span data-stu-id="98a93-157">Target Resource Name</span></span> | <span data-ttu-id="98a93-158">The name of the target resource.</span><span class="sxs-lookup"><span data-stu-id="98a93-158">The name of the target resource.</span></span> <span data-ttu-id="98a93-159">It can be an application name, a role name, a user principal name, or a service principal name.</span><span class="sxs-lookup"><span data-stu-id="98a93-159">It can be an application name, a role name, a user principal name, or a service principal name.</span></span> |
| <span data-ttu-id="98a93-160">additionalTargets</span><span class="sxs-lookup"><span data-stu-id="98a93-160">additionalTargets</span></span> | <span data-ttu-id="98a93-161">Lists any additional properties for specific operations.</span><span class="sxs-lookup"><span data-stu-id="98a93-161">Lists any additional properties for specific operations.</span></span> <span data-ttu-id="98a93-162">For example, for an update operation, the old values and the new values are listed under *targetUpdatedProperties*.</span><span class="sxs-lookup"><span data-stu-id="98a93-162">For example, for an update operation, the old values and the new values are listed under *targetUpdatedProperties*.</span></span> | 

## <a name="next-steps"></a><span data-ttu-id="98a93-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="98a93-163">Next steps</span></span>

* [<span data-ttu-id="98a93-164">Interpret sign-in logs schema in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="98a93-164">Interpret sign-in logs schema in Azure Monitor</span></span>](reference-azure-monitor-sign-ins-log-schema.md)
* [<span data-ttu-id="98a93-165">Read more about Azure diagnostics logs</span><span class="sxs-lookup"><span data-stu-id="98a93-165">Read more about Azure diagnostics logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="98a93-166">Frequently asked questions and known issues</span><span class="sxs-lookup"><span data-stu-id="98a93-166">Frequently asked questions and known issues</span></span>](overview-activity-logs-in-azure-monitor.md#frequently-asked-questions)
