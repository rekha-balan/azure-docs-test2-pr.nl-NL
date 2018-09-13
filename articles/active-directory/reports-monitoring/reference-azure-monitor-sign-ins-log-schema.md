---
title: Interpret the Azure Active Directory sign-in log schema in Azure Monitor (preview) | Microsoft Docs
description: Describe the Azure AD sign in log schema for use in Azure Monitor (preview)
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
ms.openlocfilehash: b9ad4e69c0693bc856789c52870a588671573b5c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856297"
---
# <a name="interpret-the-azure-ad-sign-in-logs-schema-in-azure-monitor-preview"></a><span data-ttu-id="16486-103">Interpret the Azure AD sign-in logs schema in Azure Monitor (preview)</span><span class="sxs-lookup"><span data-stu-id="16486-103">Interpret the Azure AD sign-in logs schema in Azure Monitor (preview)</span></span>

<span data-ttu-id="16486-104">This article describes the Azure Active Directory (Azure AD) sign-in log schema in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="16486-104">This article describes the Azure Active Directory (Azure AD) sign-in log schema in Azure Monitor.</span></span> <span data-ttu-id="16486-105">Most of the information that's related to sign-ins is provided under the *Properties* attribute of the `records` object.</span><span class="sxs-lookup"><span data-stu-id="16486-105">Most of the information that's related to sign-ins is provided under the *Properties* attribute of the `records` object.</span></span>

```json
{ 
    "records": [ 
    { 
        "time": "2018-05-16T16:09:58.4634578Z", 
        "resourceId": null, 
        "operationName": "Sign-in activity", 
        "operationVersion": "1.0", 
        "category": "SignIn", 
        "tenantId": "bf85dc9d-cb43-44a4-80c4-469e8c58249e", 
        "resultType": "50140", 
        "resultSignature": "None", 
        "resultDescription": "Other", 
        "durationMs": 0, 
        "callerIpAddress": "167.220.0.158", 
        "correlationId": "13e19598-e040-487f-bd32-d38a2cd75d9a", 
        "identity": "arvind harinder", 
        "Level": 4, 
        "location": "US", 
        "properties": { 
            "id": "0782c515-08b6-4029-a65c-29d9a3d20800", 
            "createdDateTime": "2018-05-16T16:09:58.4634578+00:00", 
            "userDisplayName": "Arvind Harinder", 
            "userPrincipalName": "ah@wingtiptoysonline.onmicrosoft.com", 
            "userId": "5b9f356d-9592-42fd-9ec4-d70963909534", 
            "appId": "c44b4083-3bb0-49c1-b47d-974e53cbdf3c", 
            "appDisplayName": "Azure Portal", 
            "ipAddress": "167.220.0.158", 
            "status": { 
                "errorCode": 50140, 
                "failureReason": "Other" 
            }, 
            "clientAppUsed": "Browser", 
            "deviceDetail": { 
                "operatingSystem": "Windows 10", 
                "browser": "Chrome 66.0.3359" 
            }, 
            "location": { 
                "city": "Sammamish", 
                "state": "Washington", 
                "countryOrRegion": "US", 
                "geoCoordinates": { 
                    "latitude": 47.66630935668945, 
                    "longitude": -122.09821319580078 
                } 
            }, 
            "correlationId": "13e19598-e040-487f-bd32-d38a2cd75d9a", 
            "conditionalAccessStatus": 2, 
            "conditionalAccessPolicies": [ 
            { 
                "id": "de7e60eb-ed89-4d73-8205-2227def6b7c9", 
                "displayName": "[billg] SharePoint limited access policy", 
                "enforcedGrantControls": [], 
                "enforcedSessionControls": [], 
                "result": 3 
            }, 
            { 
                "id": "7412a2d8-cbb1-4f1c-96cf-8410b4b8b37b", 
                "displayName": "[BillG] AIP MFA Policy", 
                "enforcedGrantControls": [], 
                "enforcedSessionControls": [], 
                "result": 3 
            }, 
            { 
                "id": "727ed8ea-059d-4d8f-aba5-c1dc500e8b06", 
                "displayName": "[billg] mfa for mail", 
                "enforcedGrantControls": [], 
                "enforcedSessionControls": [], 
                "result": 3 
            }, 
            { 
                "id": "6701123a-b4c6-48af-8565-565c8bf7cabc", 
                "displayName": "Medium signin risk block", 
                "enforcedGrantControls": [], 
                "enforcedSessionControls": [], 
                "result": 3 
            }, 
            { 
                "id": "fbafa2da-cf7f-4ec3-83cf-281188e53f76", 
                "displayName": "Require MFA for admins [Ignite talk] ", 
                "enforcedGrantControls": [], 
                "enforcedSessionControls": [], 
                "result": 3 
            }, 
            { 
                "id": "15339054-709d-4e06-a9ec-342bf043ea56", 
                "displayName": "Enhanced proofing for Azure portal [Ignite talk]", 
                "enforcedGrantControls": [], 
                "enforcedSessionControls": [], 
                "result": 3 
            }, 
            { 
                "id": "2ff9436f-bc72-4ce6-b17e-e7e51153146e", 
                "displayName": "[calebb] AIP policy", 
                "enforcedGrantControls": [], 
                "enforcedSessionControls": [], 
                "result": 3 
            }, 
            { 
                "id": "46ab586b-9447-4847-a889-e60705d96e56", 
                "displayName": "Test policy, OR", 
                "enforcedGrantControls": [], 
                "enforcedSessionControls": [], 
                "result": 3 
            }, 
            { 
                "id": "ceb6e17e-a5d0-4b3a-a150-6c2be2d5b0e9", 
                "displayName": "mm policy with Duo", 
                "enforcedGrantControls": [ 
                    "Require Duo Mfa" 
                ], 
            "enforcedSessionControls": [], 
            "result": 2 
            }, 
            ], 
            "isRisky": false 
            } 
        } 
    } 
```

## <a name="field-descriptions"></a><span data-ttu-id="16486-106">Field descriptions</span><span class="sxs-lookup"><span data-stu-id="16486-106">Field descriptions</span></span>

| <span data-ttu-id="16486-107">Field name</span><span class="sxs-lookup"><span data-stu-id="16486-107">Field name</span></span> | <span data-ttu-id="16486-108">Description</span><span class="sxs-lookup"><span data-stu-id="16486-108">Description</span></span> |
|------------|-------------|
| <span data-ttu-id="16486-109">Time</span><span class="sxs-lookup"><span data-stu-id="16486-109">Time</span></span> | <span data-ttu-id="16486-110">The date and time, in UTC.</span><span class="sxs-lookup"><span data-stu-id="16486-110">The date and time, in UTC.</span></span> |
| <span data-ttu-id="16486-111">ResourceId</span><span class="sxs-lookup"><span data-stu-id="16486-111">ResourceId</span></span> | <span data-ttu-id="16486-112">This value is unmapped, and you can safely ignore this field.</span><span class="sxs-lookup"><span data-stu-id="16486-112">This value is unmapped, and you can safely ignore this field.</span></span>  |
| <span data-ttu-id="16486-113">OperationName</span><span class="sxs-lookup"><span data-stu-id="16486-113">OperationName</span></span> | <span data-ttu-id="16486-114">For sign-ins, this value is always *Sign-in activity*.</span><span class="sxs-lookup"><span data-stu-id="16486-114">For sign-ins, this value is always *Sign-in activity*.</span></span> |
| <span data-ttu-id="16486-115">OperationVersion</span><span class="sxs-lookup"><span data-stu-id="16486-115">OperationVersion</span></span> | <span data-ttu-id="16486-116">The REST API version that's requested by the client.</span><span class="sxs-lookup"><span data-stu-id="16486-116">The REST API version that's requested by the client.</span></span> |
| <span data-ttu-id="16486-117">Category</span><span class="sxs-lookup"><span data-stu-id="16486-117">Category</span></span> | <span data-ttu-id="16486-118">For sign-ins, this value is always *SignIn*.</span><span class="sxs-lookup"><span data-stu-id="16486-118">For sign-ins, this value is always *SignIn*.</span></span> | 
| <span data-ttu-id="16486-119">TenantId</span><span class="sxs-lookup"><span data-stu-id="16486-119">TenantId</span></span> | <span data-ttu-id="16486-120">The tenant GUID that's associated with the logs.</span><span class="sxs-lookup"><span data-stu-id="16486-120">The tenant GUID that's associated with the logs.</span></span> |
| <span data-ttu-id="16486-121">ResultType</span><span class="sxs-lookup"><span data-stu-id="16486-121">ResultType</span></span> | <span data-ttu-id="16486-122">The result of the sign-in operation can be *Success* or *Failure*.</span><span class="sxs-lookup"><span data-stu-id="16486-122">The result of the sign-in operation can be *Success* or *Failure*.</span></span> | 
| <span data-ttu-id="16486-123">ResultSignature</span><span class="sxs-lookup"><span data-stu-id="16486-123">ResultSignature</span></span> | <span data-ttu-id="16486-124">Contains the error code, if any, for the sign-in operation.</span><span class="sxs-lookup"><span data-stu-id="16486-124">Contains the error code, if any, for the sign-in operation.</span></span> |
| <span data-ttu-id="16486-125">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="16486-125">ResultDescription</span></span> | <span data-ttu-id="16486-126">Provides the error description for the sign-in operation.</span><span class="sxs-lookup"><span data-stu-id="16486-126">Provides the error description for the sign-in operation.</span></span> |
| <span data-ttu-id="16486-127">DurationMs</span><span class="sxs-lookup"><span data-stu-id="16486-127">DurationMs</span></span> |  <span data-ttu-id="16486-128">This value is unmapped, and you can safely ignore this field.</span><span class="sxs-lookup"><span data-stu-id="16486-128">This value is unmapped, and you can safely ignore this field.</span></span>|
| <span data-ttu-id="16486-129">CallerIpAddress</span><span class="sxs-lookup"><span data-stu-id="16486-129">CallerIpAddress</span></span> | <span data-ttu-id="16486-130">The IP address of the client that made the request.</span><span class="sxs-lookup"><span data-stu-id="16486-130">The IP address of the client that made the request.</span></span> | 
| <span data-ttu-id="16486-131">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="16486-131">CorrelationId</span></span> | <span data-ttu-id="16486-132">The optional GUID that's passed by the client.</span><span class="sxs-lookup"><span data-stu-id="16486-132">The optional GUID that's passed by the client.</span></span> <span data-ttu-id="16486-133">This value can help correlate client-side operations with server-side operations, and it's useful when you're tracking logs that span services.</span><span class="sxs-lookup"><span data-stu-id="16486-133">This value can help correlate client-side operations with server-side operations, and it's useful when you're tracking logs that span services.</span></span> |
| <span data-ttu-id="16486-134">Identity</span><span class="sxs-lookup"><span data-stu-id="16486-134">Identity</span></span> | <span data-ttu-id="16486-135">The identity from the token that was presented when you made the request.</span><span class="sxs-lookup"><span data-stu-id="16486-135">The identity from the token that was presented when you made the request.</span></span> <span data-ttu-id="16486-136">It can be a user account, system account, or service principal.</span><span class="sxs-lookup"><span data-stu-id="16486-136">It can be a user account, system account, or service principal.</span></span> |
| <span data-ttu-id="16486-137">Level</span><span class="sxs-lookup"><span data-stu-id="16486-137">Level</span></span> | <span data-ttu-id="16486-138">Provides the type of message.</span><span class="sxs-lookup"><span data-stu-id="16486-138">Provides the type of message.</span></span> <span data-ttu-id="16486-139">For audit, it's always *Informational*.</span><span class="sxs-lookup"><span data-stu-id="16486-139">For audit, it's always *Informational*.</span></span> |
| <span data-ttu-id="16486-140">Location</span><span class="sxs-lookup"><span data-stu-id="16486-140">Location</span></span> | <span data-ttu-id="16486-141">Provides the location of the sign-in activity.</span><span class="sxs-lookup"><span data-stu-id="16486-141">Provides the location of the sign-in activity.</span></span> |
| <span data-ttu-id="16486-142">Properties</span><span class="sxs-lookup"><span data-stu-id="16486-142">Properties</span></span> | <span data-ttu-id="16486-143">Lists all the properties that are associated with sign-ins. For more information, see [Microsoft Graph API Reference](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/signin).</span><span class="sxs-lookup"><span data-stu-id="16486-143">Lists all the properties that are associated with sign-ins. For more information, see [Microsoft Graph API Reference](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/signin).</span></span> <span data-ttu-id="16486-144">This schema uses the same attribute names as the sign-in resource, for readability.</span><span class="sxs-lookup"><span data-stu-id="16486-144">This schema uses the same attribute names as the sign-in resource, for readability.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16486-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="16486-145">Next steps</span></span>

* [<span data-ttu-id="16486-146">Interpret audit logs schema in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="16486-146">Interpret audit logs schema in Azure Monitor</span></span>](reference-azure-monitor-audit-log-schema.md)
* [<span data-ttu-id="16486-147">Read more about Azure diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="16486-147">Read more about Azure diagnostic logs</span></span>](../../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)
