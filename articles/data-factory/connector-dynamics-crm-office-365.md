---
title: Copy data from and to Dynamics CRM or Dynamics 365 (Common Data Service) by using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Microsoft Dynamics CRM or Microsoft Dynamics 365 (Common Data Service) to supported sink data stores, or from supported source data stores to Dynamics CRM or Dynamics 365, by using a copy activity in a data factory pipeline.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/02/2018
ms.author: jingwang
ms.openlocfilehash: e4ebddc35b402d7a8997d899ce97577e93a27b84
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864730"
---
# <a name="copy-data-from-and-to-dynamics-365-common-data-service-or-dynamics-crm-by-using-azure-data-factory"></a><span data-ttu-id="f4f87-103">Copy data from and to Dynamics 365 (Common Data Service) or Dynamics CRM by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f4f87-103">Copy data from and to Dynamics 365 (Common Data Service) or Dynamics CRM by using Azure Data Factory</span></span>

<span data-ttu-id="f4f87-104">This article outlines how to use Copy Activity in Azure Data Factory to copy data from and to Microsoft Dynamics 365 or Microsoft Dynamics CRM.</span><span class="sxs-lookup"><span data-stu-id="f4f87-104">This article outlines how to use Copy Activity in Azure Data Factory to copy data from and to Microsoft Dynamics 365 or Microsoft Dynamics CRM.</span></span> <span data-ttu-id="f4f87-105">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="f4f87-105">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of Copy Activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="f4f87-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="f4f87-106">Supported capabilities</span></span>

<span data-ttu-id="f4f87-107">You can copy data from Dynamics 365 (Common Data Service) or Dynamics CRM to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="f4f87-107">You can copy data from Dynamics 365 (Common Data Service) or Dynamics CRM to any supported sink data store.</span></span> <span data-ttu-id="f4f87-108">You also can copy data from any supported source data store to Dynamics 365 (Common Data Service) or Dynamics CRM.</span><span class="sxs-lookup"><span data-stu-id="f4f87-108">You also can copy data from any supported source data store to Dynamics 365 (Common Data Service) or Dynamics CRM.</span></span> <span data-ttu-id="f4f87-109">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="f4f87-109">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="f4f87-110">This Dynamics connector supports the following Dynamics versions and authentication types.</span><span class="sxs-lookup"><span data-stu-id="f4f87-110">This Dynamics connector supports the following Dynamics versions and authentication types.</span></span> <span data-ttu-id="f4f87-111">(IFD is short for internet-facing deployment.)</span><span class="sxs-lookup"><span data-stu-id="f4f87-111">(IFD is short for internet-facing deployment.)</span></span>

| <span data-ttu-id="f4f87-112">Dynamics versions</span><span class="sxs-lookup"><span data-stu-id="f4f87-112">Dynamics versions</span></span> | <span data-ttu-id="f4f87-113">Authentication types</span><span class="sxs-lookup"><span data-stu-id="f4f87-113">Authentication types</span></span> | <span data-ttu-id="f4f87-114">Linked service samples</span><span class="sxs-lookup"><span data-stu-id="f4f87-114">Linked service samples</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f4f87-115">Dynamics 365 online</span><span class="sxs-lookup"><span data-stu-id="f4f87-115">Dynamics 365 online</span></span> <br> <span data-ttu-id="f4f87-116">Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="f4f87-116">Dynamics CRM Online</span></span> | <span data-ttu-id="f4f87-117">Office365</span><span class="sxs-lookup"><span data-stu-id="f4f87-117">Office365</span></span> | [<span data-ttu-id="f4f87-118">Dynamics online + Office365 auth</span><span class="sxs-lookup"><span data-stu-id="f4f87-118">Dynamics online + Office365 auth</span></span>](#dynamics-365-and-dynamics-crm-online) |
| <span data-ttu-id="f4f87-119">Dynamics 365 on-premises with IFD</span><span class="sxs-lookup"><span data-stu-id="f4f87-119">Dynamics 365 on-premises with IFD</span></span> <br> <span data-ttu-id="f4f87-120">Dynamics CRM 2016 on-premises with IFD</span><span class="sxs-lookup"><span data-stu-id="f4f87-120">Dynamics CRM 2016 on-premises with IFD</span></span> <br> <span data-ttu-id="f4f87-121">Dynamics CRM 2015 on-premises with IFD</span><span class="sxs-lookup"><span data-stu-id="f4f87-121">Dynamics CRM 2015 on-premises with IFD</span></span> | <span data-ttu-id="f4f87-122">IFD</span><span class="sxs-lookup"><span data-stu-id="f4f87-122">IFD</span></span> | [<span data-ttu-id="f4f87-123">Dynamics on-premises with IFD + IFD auth</span><span class="sxs-lookup"><span data-stu-id="f4f87-123">Dynamics on-premises with IFD + IFD auth</span></span>](#dynamics-365-and-dynamics-crm-on-premises-with-ifd) |

<span data-ttu-id="f4f87-124">For Dynamics 365 specifically, the following application types are supported:</span><span class="sxs-lookup"><span data-stu-id="f4f87-124">For Dynamics 365 specifically, the following application types are supported:</span></span>

- <span data-ttu-id="f4f87-125">Dynamics 365 for Sales</span><span class="sxs-lookup"><span data-stu-id="f4f87-125">Dynamics 365 for Sales</span></span>
- <span data-ttu-id="f4f87-126">Dynamics 365 for Customer Service</span><span class="sxs-lookup"><span data-stu-id="f4f87-126">Dynamics 365 for Customer Service</span></span>
- <span data-ttu-id="f4f87-127">Dynamics 365 for Field Service</span><span class="sxs-lookup"><span data-stu-id="f4f87-127">Dynamics 365 for Field Service</span></span>
- <span data-ttu-id="f4f87-128">Dynamics 365 for Project Service Automation</span><span class="sxs-lookup"><span data-stu-id="f4f87-128">Dynamics 365 for Project Service Automation</span></span>
- <span data-ttu-id="f4f87-129">Dynamics 365 for Marketing</span><span class="sxs-lookup"><span data-stu-id="f4f87-129">Dynamics 365 for Marketing</span></span>

<span data-ttu-id="f4f87-130">Other application types e.g. Operations and Finance, Talent, etc. are not supported.</span><span class="sxs-lookup"><span data-stu-id="f4f87-130">Other application types e.g. Operations and Finance, Talent, etc. are not supported.</span></span>

## <a name="get-started"></a><span data-ttu-id="f4f87-131">Get started</span><span class="sxs-lookup"><span data-stu-id="f4f87-131">Get started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="f4f87-132">The following sections provide details about properties that are used to define Data Factory entities specific to Dynamics.</span><span class="sxs-lookup"><span data-stu-id="f4f87-132">The following sections provide details about properties that are used to define Data Factory entities specific to Dynamics.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f4f87-133">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="f4f87-133">Linked service properties</span></span>

<span data-ttu-id="f4f87-134">The following properties are supported for the Dynamics linked service.</span><span class="sxs-lookup"><span data-stu-id="f4f87-134">The following properties are supported for the Dynamics linked service.</span></span>

### <a name="dynamics-365-and-dynamics-crm-online"></a><span data-ttu-id="f4f87-135">Dynamics 365 and Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="f4f87-135">Dynamics 365 and Dynamics CRM Online</span></span>

| <span data-ttu-id="f4f87-136">Property</span><span class="sxs-lookup"><span data-stu-id="f4f87-136">Property</span></span> | <span data-ttu-id="f4f87-137">Description</span><span class="sxs-lookup"><span data-stu-id="f4f87-137">Description</span></span> | <span data-ttu-id="f4f87-138">Required</span><span class="sxs-lookup"><span data-stu-id="f4f87-138">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f4f87-139">type</span><span class="sxs-lookup"><span data-stu-id="f4f87-139">type</span></span> | <span data-ttu-id="f4f87-140">The type property must be set to **Dynamics**.</span><span class="sxs-lookup"><span data-stu-id="f4f87-140">The type property must be set to **Dynamics**.</span></span> | <span data-ttu-id="f4f87-141">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-141">Yes</span></span> |
| <span data-ttu-id="f4f87-142">deploymentType</span><span class="sxs-lookup"><span data-stu-id="f4f87-142">deploymentType</span></span> | <span data-ttu-id="f4f87-143">The deployment type of the Dynamics instance.</span><span class="sxs-lookup"><span data-stu-id="f4f87-143">The deployment type of the Dynamics instance.</span></span> <span data-ttu-id="f4f87-144">It must be **"Online"** for Dynamics online.</span><span class="sxs-lookup"><span data-stu-id="f4f87-144">It must be **"Online"** for Dynamics online.</span></span> | <span data-ttu-id="f4f87-145">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-145">Yes</span></span> |
| <span data-ttu-id="f4f87-146">serviceUri</span><span class="sxs-lookup"><span data-stu-id="f4f87-146">serviceUri</span></span> | <span data-ttu-id="f4f87-147">The service URL of your Dynamics instance, e.g. `https://adfdynamics.crm.dynamics.com`.</span><span class="sxs-lookup"><span data-stu-id="f4f87-147">The service URL of your Dynamics instance, e.g. `https://adfdynamics.crm.dynamics.com`.</span></span> | <span data-ttu-id="f4f87-148">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-148">Yes</span></span> |
| <span data-ttu-id="f4f87-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f4f87-149">authenticationType</span></span> | <span data-ttu-id="f4f87-150">The authentication type to connect to a Dynamics server.</span><span class="sxs-lookup"><span data-stu-id="f4f87-150">The authentication type to connect to a Dynamics server.</span></span> <span data-ttu-id="f4f87-151">Specify **"Office365"** for Dynamics online.</span><span class="sxs-lookup"><span data-stu-id="f4f87-151">Specify **"Office365"** for Dynamics online.</span></span> | <span data-ttu-id="f4f87-152">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-152">Yes</span></span> |
| <span data-ttu-id="f4f87-153">username</span><span class="sxs-lookup"><span data-stu-id="f4f87-153">username</span></span> | <span data-ttu-id="f4f87-154">Specify the user name to connect to Dynamics.</span><span class="sxs-lookup"><span data-stu-id="f4f87-154">Specify the user name to connect to Dynamics.</span></span> | <span data-ttu-id="f4f87-155">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-155">Yes</span></span> |
| <span data-ttu-id="f4f87-156">password</span><span class="sxs-lookup"><span data-stu-id="f4f87-156">password</span></span> | <span data-ttu-id="f4f87-157">Specify the password for the user account you specified for username.</span><span class="sxs-lookup"><span data-stu-id="f4f87-157">Specify the password for the user account you specified for username.</span></span> <span data-ttu-id="f4f87-158">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="f4f87-158">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="f4f87-159">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-159">Yes</span></span> |
| <span data-ttu-id="f4f87-160">connectVia</span><span class="sxs-lookup"><span data-stu-id="f4f87-160">connectVia</span></span> | <span data-ttu-id="f4f87-161">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="f4f87-161">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="f4f87-162">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="f4f87-162">If not specified, it uses the default Azure Integration Runtime.</span></span> | <span data-ttu-id="f4f87-163">No for source, Yes for sink if the source linked service doesn't have an integration runtime</span><span class="sxs-lookup"><span data-stu-id="f4f87-163">No for source, Yes for sink if the source linked service doesn't have an integration runtime</span></span> |

>[!IMPORTANT]
><span data-ttu-id="f4f87-164">When you copy data into Dynamics, the default Azure Integration Runtime can't be used to execute copy.</span><span class="sxs-lookup"><span data-stu-id="f4f87-164">When you copy data into Dynamics, the default Azure Integration Runtime can't be used to execute copy.</span></span> <span data-ttu-id="f4f87-165">In other words, if your source linked service doesn't have a specified integration runtime, explicitly [create an Azure Integration Runtime](create-azure-integration-runtime.md#create-azure-ir) with a location near your Dynamics instance.</span><span class="sxs-lookup"><span data-stu-id="f4f87-165">In other words, if your source linked service doesn't have a specified integration runtime, explicitly [create an Azure Integration Runtime](create-azure-integration-runtime.md#create-azure-ir) with a location near your Dynamics instance.</span></span> <span data-ttu-id="f4f87-166">Associate it in the Dynamics linked service as in the following example.</span><span class="sxs-lookup"><span data-stu-id="f4f87-166">Associate it in the Dynamics linked service as in the following example.</span></span>

>[!NOTE]
><span data-ttu-id="f4f87-167">The Dynamics connector used to use optional "organizationName" property to identify your Dynamics CRM/365 Online instance.</span><span class="sxs-lookup"><span data-stu-id="f4f87-167">The Dynamics connector used to use optional "organizationName" property to identify your Dynamics CRM/365 Online instance.</span></span> <span data-ttu-id="f4f87-168">While it keeps working, you are suggested to specify the new "serviceUri" property instead to gain better performance for instance discovery.</span><span class="sxs-lookup"><span data-stu-id="f4f87-168">While it keeps working, you are suggested to specify the new "serviceUri" property instead to gain better performance for instance discovery.</span></span>

<span data-ttu-id="f4f87-169">**Example: Dynamics online using Office365 authentication**</span><span class="sxs-lookup"><span data-stu-id="f4f87-169">**Example: Dynamics online using Office365 authentication**</span></span>

```json
{
    "name": "DynamicsLinkedService",
    "properties": {
        "type": "Dynamics",
        "description": "Dynamics online linked service using Office365 authentication",
        "typeProperties": {
            "deploymentType": "Online",
            "serviceUri": "https://adfdynamics.crm.dynamics.com",
            "authenticationType": "Office365",
            "username": "test@contoso.onmicrosoft.com",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

### <a name="dynamics-365-and-dynamics-crm-on-premises-with-ifd"></a><span data-ttu-id="f4f87-170">Dynamics 365 and Dynamics CRM on-premises with IFD</span><span class="sxs-lookup"><span data-stu-id="f4f87-170">Dynamics 365 and Dynamics CRM on-premises with IFD</span></span>

<span data-ttu-id="f4f87-171">*Additional properties that compare to Dynamics online are "hostName" and "port".*</span><span class="sxs-lookup"><span data-stu-id="f4f87-171">*Additional properties that compare to Dynamics online are "hostName" and "port".*</span></span>

| <span data-ttu-id="f4f87-172">Property</span><span class="sxs-lookup"><span data-stu-id="f4f87-172">Property</span></span> | <span data-ttu-id="f4f87-173">Description</span><span class="sxs-lookup"><span data-stu-id="f4f87-173">Description</span></span> | <span data-ttu-id="f4f87-174">Required</span><span class="sxs-lookup"><span data-stu-id="f4f87-174">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f4f87-175">type</span><span class="sxs-lookup"><span data-stu-id="f4f87-175">type</span></span> | <span data-ttu-id="f4f87-176">The type property must be set to **Dynamics**.</span><span class="sxs-lookup"><span data-stu-id="f4f87-176">The type property must be set to **Dynamics**.</span></span> | <span data-ttu-id="f4f87-177">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-177">Yes</span></span> |
| <span data-ttu-id="f4f87-178">deploymentType</span><span class="sxs-lookup"><span data-stu-id="f4f87-178">deploymentType</span></span> | <span data-ttu-id="f4f87-179">The deployment type of the Dynamics instance.</span><span class="sxs-lookup"><span data-stu-id="f4f87-179">The deployment type of the Dynamics instance.</span></span> <span data-ttu-id="f4f87-180">It must be **"OnPremisesWithIfd"** for Dynamics on-premises with IFD.</span><span class="sxs-lookup"><span data-stu-id="f4f87-180">It must be **"OnPremisesWithIfd"** for Dynamics on-premises with IFD.</span></span>| <span data-ttu-id="f4f87-181">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-181">Yes</span></span> |
| <span data-ttu-id="f4f87-182">hostName</span><span class="sxs-lookup"><span data-stu-id="f4f87-182">hostName</span></span> | <span data-ttu-id="f4f87-183">The host name of the on-premises Dynamics server.</span><span class="sxs-lookup"><span data-stu-id="f4f87-183">The host name of the on-premises Dynamics server.</span></span> | <span data-ttu-id="f4f87-184">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-184">Yes</span></span> |
| <span data-ttu-id="f4f87-185">port</span><span class="sxs-lookup"><span data-stu-id="f4f87-185">port</span></span> | <span data-ttu-id="f4f87-186">The port of the on-premises Dynamics server.</span><span class="sxs-lookup"><span data-stu-id="f4f87-186">The port of the on-premises Dynamics server.</span></span> | <span data-ttu-id="f4f87-187">No, default is 443</span><span class="sxs-lookup"><span data-stu-id="f4f87-187">No, default is 443</span></span> |
| <span data-ttu-id="f4f87-188">organizationName</span><span class="sxs-lookup"><span data-stu-id="f4f87-188">organizationName</span></span> | <span data-ttu-id="f4f87-189">The organization name of the Dynamics instance.</span><span class="sxs-lookup"><span data-stu-id="f4f87-189">The organization name of the Dynamics instance.</span></span> | <span data-ttu-id="f4f87-190">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-190">Yes</span></span> |
| <span data-ttu-id="f4f87-191">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f4f87-191">authenticationType</span></span> | <span data-ttu-id="f4f87-192">The authentication type to connect to the Dynamics server.</span><span class="sxs-lookup"><span data-stu-id="f4f87-192">The authentication type to connect to the Dynamics server.</span></span> <span data-ttu-id="f4f87-193">Specify **"Ifd"** for Dynamics on-premises with IFD.</span><span class="sxs-lookup"><span data-stu-id="f4f87-193">Specify **"Ifd"** for Dynamics on-premises with IFD.</span></span> | <span data-ttu-id="f4f87-194">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-194">Yes</span></span> |
| <span data-ttu-id="f4f87-195">username</span><span class="sxs-lookup"><span data-stu-id="f4f87-195">username</span></span> | <span data-ttu-id="f4f87-196">Specify the user name to connect to Dynamics.</span><span class="sxs-lookup"><span data-stu-id="f4f87-196">Specify the user name to connect to Dynamics.</span></span> | <span data-ttu-id="f4f87-197">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-197">Yes</span></span> |
| <span data-ttu-id="f4f87-198">password</span><span class="sxs-lookup"><span data-stu-id="f4f87-198">password</span></span> | <span data-ttu-id="f4f87-199">Specify the password for the user account you specified for username.</span><span class="sxs-lookup"><span data-stu-id="f4f87-199">Specify the password for the user account you specified for username.</span></span> <span data-ttu-id="f4f87-200">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let the copy activity pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="f4f87-200">You can choose to mark this field as a SecureString to store it securely in ADF, or store password in Azure Key Vault and let the copy activity pull from there when performing data copy - learn more from [Store credentials in Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="f4f87-201">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-201">Yes</span></span> |
| <span data-ttu-id="f4f87-202">connectVia</span><span class="sxs-lookup"><span data-stu-id="f4f87-202">connectVia</span></span> | <span data-ttu-id="f4f87-203">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="f4f87-203">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="f4f87-204">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="f4f87-204">If not specified, it uses the default Azure Integration Runtime.</span></span> | <span data-ttu-id="f4f87-205">No for source, Yes for sink</span><span class="sxs-lookup"><span data-stu-id="f4f87-205">No for source, Yes for sink</span></span> |

>[!IMPORTANT]
><span data-ttu-id="f4f87-206">To copy data into Dynamics, explicitly [create an Azure Integration Runtime](create-azure-integration-runtime.md#create-azure-ir) with the location near your Dynamics instance.</span><span class="sxs-lookup"><span data-stu-id="f4f87-206">To copy data into Dynamics, explicitly [create an Azure Integration Runtime](create-azure-integration-runtime.md#create-azure-ir) with the location near your Dynamics instance.</span></span> <span data-ttu-id="f4f87-207">Associate it in the linked service as in the following example.</span><span class="sxs-lookup"><span data-stu-id="f4f87-207">Associate it in the linked service as in the following example.</span></span>

<span data-ttu-id="f4f87-208">**Example: Dynamics on-premises with IFD using IFD authentication**</span><span class="sxs-lookup"><span data-stu-id="f4f87-208">**Example: Dynamics on-premises with IFD using IFD authentication**</span></span>

```json
{
    "name": "DynamicsLinkedService",
    "properties": {
        "type": "Dynamics",
        "description": "Dynamics on-premises with IFD linked service using IFD authentication",
        "typeProperties": {
            "deploymentType": "OnPremisesWithIFD",
            "hostName": "contosodynamicsserver.contoso.com",
            "port": 443,
            "organizationName": "admsDynamicsTest",
            "authenticationType": "Ifd",
            "username": "test@contoso.onmicrosoft.com",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="f4f87-209">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="f4f87-209">Dataset properties</span></span>

<span data-ttu-id="f4f87-210">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="f4f87-210">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="f4f87-211">This section provides a list of properties supported by Dynamics dataset.</span><span class="sxs-lookup"><span data-stu-id="f4f87-211">This section provides a list of properties supported by Dynamics dataset.</span></span>

<span data-ttu-id="f4f87-212">To copy data from and to Dynamics, set the type property of the dataset to **DynamicsEntity**.</span><span class="sxs-lookup"><span data-stu-id="f4f87-212">To copy data from and to Dynamics, set the type property of the dataset to **DynamicsEntity**.</span></span> <span data-ttu-id="f4f87-213">The following properties are supported.</span><span class="sxs-lookup"><span data-stu-id="f4f87-213">The following properties are supported.</span></span>

| <span data-ttu-id="f4f87-214">Property</span><span class="sxs-lookup"><span data-stu-id="f4f87-214">Property</span></span> | <span data-ttu-id="f4f87-215">Description</span><span class="sxs-lookup"><span data-stu-id="f4f87-215">Description</span></span> | <span data-ttu-id="f4f87-216">Required</span><span class="sxs-lookup"><span data-stu-id="f4f87-216">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f4f87-217">type</span><span class="sxs-lookup"><span data-stu-id="f4f87-217">type</span></span> | <span data-ttu-id="f4f87-218">The type property of the dataset must be set to **DynamicsEntity**.</span><span class="sxs-lookup"><span data-stu-id="f4f87-218">The type property of the dataset must be set to **DynamicsEntity**.</span></span> |<span data-ttu-id="f4f87-219">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-219">Yes</span></span> |
| <span data-ttu-id="f4f87-220">entityName</span><span class="sxs-lookup"><span data-stu-id="f4f87-220">entityName</span></span> | <span data-ttu-id="f4f87-221">The logical name of the entity to retrieve.</span><span class="sxs-lookup"><span data-stu-id="f4f87-221">The logical name of the entity to retrieve.</span></span> | <span data-ttu-id="f4f87-222">No for source (if "query" in the activity source is specified), Yes for sink</span><span class="sxs-lookup"><span data-stu-id="f4f87-222">No for source (if "query" in the activity source is specified), Yes for sink</span></span> |

> [!IMPORTANT]
>- <span data-ttu-id="f4f87-223">When you copy data from Dynamics, the "structure" section is required in the Dynamics dataset.</span><span class="sxs-lookup"><span data-stu-id="f4f87-223">When you copy data from Dynamics, the "structure" section is required in the Dynamics dataset.</span></span> <span data-ttu-id="f4f87-224">It defines the column name and data type for Dynamics data that you want to copy over.</span><span class="sxs-lookup"><span data-stu-id="f4f87-224">It defines the column name and data type for Dynamics data that you want to copy over.</span></span> <span data-ttu-id="f4f87-225">To learn more, see [Dataset structure](concepts-datasets-linked-services.md#dataset-structure) and [Data type mapping for Dynamics](#data-type-mapping-for-dynamics).</span><span class="sxs-lookup"><span data-stu-id="f4f87-225">To learn more, see [Dataset structure](concepts-datasets-linked-services.md#dataset-structure) and [Data type mapping for Dynamics](#data-type-mapping-for-dynamics).</span></span>
>- <span data-ttu-id="f4f87-226">When you copy data to Dynamics, the "structure" section is optional in the Dynamics dataset.</span><span class="sxs-lookup"><span data-stu-id="f4f87-226">When you copy data to Dynamics, the "structure" section is optional in the Dynamics dataset.</span></span> <span data-ttu-id="f4f87-227">Which columns to copy into is determined by the source data schema.</span><span class="sxs-lookup"><span data-stu-id="f4f87-227">Which columns to copy into is determined by the source data schema.</span></span> <span data-ttu-id="f4f87-228">If your source is a CSV file without a header, in the input dataset, specify the "structure" with the column name and data type.</span><span class="sxs-lookup"><span data-stu-id="f4f87-228">If your source is a CSV file without a header, in the input dataset, specify the "structure" with the column name and data type.</span></span> <span data-ttu-id="f4f87-229">They map to fields in the CSV file one by one in order.</span><span class="sxs-lookup"><span data-stu-id="f4f87-229">They map to fields in the CSV file one by one in order.</span></span>

<span data-ttu-id="f4f87-230">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f4f87-230">**Example:**</span></span>

```json
{
    "name": "DynamicsDataset",
    "properties": {
        "type": "DynamicsEntity",
        "structure": [
            {
                "name": "accountid",
                "type": "Guid"
            },
            {
                "name": "name",
                "type": "String"
            },
            {
                "name": "marketingonly",
                "type": "Boolean"
            },
            {
                "name": "modifiedon",
                "type": "Datetime"
            }
        ],
        "typeProperties": {
            "entityName": "account"
        },
        "linkedServiceName": {
            "referenceName": "<Dynamics linked service name>",
            "type": "linkedservicereference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="f4f87-231">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="f4f87-231">Copy activity properties</span></span>

<span data-ttu-id="f4f87-232">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="f4f87-232">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="f4f87-233">This section provides a list of properties supported by Dynamics source and sink types.</span><span class="sxs-lookup"><span data-stu-id="f4f87-233">This section provides a list of properties supported by Dynamics source and sink types.</span></span>

### <a name="dynamics-as-a-source-type"></a><span data-ttu-id="f4f87-234">Dynamics as a source type</span><span class="sxs-lookup"><span data-stu-id="f4f87-234">Dynamics as a source type</span></span>

<span data-ttu-id="f4f87-235">To copy data from Dynamics, set the source type in the copy activity to **DynamicsSource**.</span><span class="sxs-lookup"><span data-stu-id="f4f87-235">To copy data from Dynamics, set the source type in the copy activity to **DynamicsSource**.</span></span> <span data-ttu-id="f4f87-236">The following properties are supported in the copy activity **source** section.</span><span class="sxs-lookup"><span data-stu-id="f4f87-236">The following properties are supported in the copy activity **source** section.</span></span>

| <span data-ttu-id="f4f87-237">Property</span><span class="sxs-lookup"><span data-stu-id="f4f87-237">Property</span></span> | <span data-ttu-id="f4f87-238">Description</span><span class="sxs-lookup"><span data-stu-id="f4f87-238">Description</span></span> | <span data-ttu-id="f4f87-239">Required</span><span class="sxs-lookup"><span data-stu-id="f4f87-239">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f4f87-240">type</span><span class="sxs-lookup"><span data-stu-id="f4f87-240">type</span></span> | <span data-ttu-id="f4f87-241">The type property of the copy activity source must be set to **DynamicsSource**.</span><span class="sxs-lookup"><span data-stu-id="f4f87-241">The type property of the copy activity source must be set to **DynamicsSource**.</span></span> | <span data-ttu-id="f4f87-242">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-242">Yes</span></span> |
| <span data-ttu-id="f4f87-243">query</span><span class="sxs-lookup"><span data-stu-id="f4f87-243">query</span></span> | <span data-ttu-id="f4f87-244">FetchXML is a proprietary query language that is used in Dynamics (online and on-premises).</span><span class="sxs-lookup"><span data-stu-id="f4f87-244">FetchXML is a proprietary query language that is used in Dynamics (online and on-premises).</span></span> <span data-ttu-id="f4f87-245">See the following example.</span><span class="sxs-lookup"><span data-stu-id="f4f87-245">See the following example.</span></span> <span data-ttu-id="f4f87-246">To learn more, see [Build queries with FeachXML](https://msdn.microsoft.com/library/gg328332.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4f87-246">To learn more, see [Build queries with FeachXML](https://msdn.microsoft.com/library/gg328332.aspx).</span></span> | <span data-ttu-id="f4f87-247">No (if "entityName" in the dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="f4f87-247">No (if "entityName" in the dataset is specified)</span></span> |

>[!NOTE]
><span data-ttu-id="f4f87-248">The PK column will always be copied out even if the column projection you configure in the FetchXML query doesn't contain it.</span><span class="sxs-lookup"><span data-stu-id="f4f87-248">The PK column will always be copied out even if the column projection you configure in the FetchXML query doesn't contain it.</span></span>

<span data-ttu-id="f4f87-249">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f4f87-249">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromDynamics",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Dynamics input dataset>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "DynamicsSource",
                "query": "<FetchXML Query>"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="sample-fetchxml-query"></a><span data-ttu-id="f4f87-250">Sample FetchXML query</span><span class="sxs-lookup"><span data-stu-id="f4f87-250">Sample FetchXML query</span></span>

```xml
<fetch>
  <entity name="account">
    <attribute name="accountid" />
    <attribute name="name" />
    <attribute name="marketingonly" />
    <attribute name="modifiedon" />
    <order attribute="modifiedon" descending="false" />
    <filter type="and">
      <condition attribute ="modifiedon" operator="between">
        <value>2017-03-10 18:40:00z</value>
        <value>2017-03-12 20:40:00z</value>
      </condition>
    </filter>
  </entity>
</fetch>
```

### <a name="dynamics-as-a-sink-type"></a><span data-ttu-id="f4f87-251">Dynamics as a sink type</span><span class="sxs-lookup"><span data-stu-id="f4f87-251">Dynamics as a sink type</span></span>

<span data-ttu-id="f4f87-252">To copy data to Dynamics, set the sink type in the copy activity to **DynamicsSink**.</span><span class="sxs-lookup"><span data-stu-id="f4f87-252">To copy data to Dynamics, set the sink type in the copy activity to **DynamicsSink**.</span></span> <span data-ttu-id="f4f87-253">The following properties are supported in the copy activity **sink** section.</span><span class="sxs-lookup"><span data-stu-id="f4f87-253">The following properties are supported in the copy activity **sink** section.</span></span>

| <span data-ttu-id="f4f87-254">Property</span><span class="sxs-lookup"><span data-stu-id="f4f87-254">Property</span></span> | <span data-ttu-id="f4f87-255">Description</span><span class="sxs-lookup"><span data-stu-id="f4f87-255">Description</span></span> | <span data-ttu-id="f4f87-256">Required</span><span class="sxs-lookup"><span data-stu-id="f4f87-256">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f4f87-257">type</span><span class="sxs-lookup"><span data-stu-id="f4f87-257">type</span></span> | <span data-ttu-id="f4f87-258">The type property of the copy activity sink must be set to **DynamicsSink**.</span><span class="sxs-lookup"><span data-stu-id="f4f87-258">The type property of the copy activity sink must be set to **DynamicsSink**.</span></span> | <span data-ttu-id="f4f87-259">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-259">Yes</span></span> |
| <span data-ttu-id="f4f87-260">writeBehavior</span><span class="sxs-lookup"><span data-stu-id="f4f87-260">writeBehavior</span></span> | <span data-ttu-id="f4f87-261">The write behavior of the operation.</span><span class="sxs-lookup"><span data-stu-id="f4f87-261">The write behavior of the operation.</span></span><br/><span data-ttu-id="f4f87-262">Allowed value is **"Upsert"**.</span><span class="sxs-lookup"><span data-stu-id="f4f87-262">Allowed value is **"Upsert"**.</span></span> | <span data-ttu-id="f4f87-263">Yes</span><span class="sxs-lookup"><span data-stu-id="f4f87-263">Yes</span></span> |
| <span data-ttu-id="f4f87-264">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="f4f87-264">writeBatchSize</span></span> | <span data-ttu-id="f4f87-265">The row count of data written to Dynamics in each batch.</span><span class="sxs-lookup"><span data-stu-id="f4f87-265">The row count of data written to Dynamics in each batch.</span></span> | <span data-ttu-id="f4f87-266">No (default is 10)</span><span class="sxs-lookup"><span data-stu-id="f4f87-266">No (default is 10)</span></span> |
| <span data-ttu-id="f4f87-267">ignoreNullValues</span><span class="sxs-lookup"><span data-stu-id="f4f87-267">ignoreNullValues</span></span> | <span data-ttu-id="f4f87-268">Indicates whether to ignore null values from input data (except key fields) during a write operation.</span><span class="sxs-lookup"><span data-stu-id="f4f87-268">Indicates whether to ignore null values from input data (except key fields) during a write operation.</span></span><br/><span data-ttu-id="f4f87-269">Allowed values are **true** and **false**.</span><span class="sxs-lookup"><span data-stu-id="f4f87-269">Allowed values are **true** and **false**.</span></span><br><span data-ttu-id="f4f87-270">- **True**: Leave the data in the destination object unchanged when you do an upsert/update operation.</span><span class="sxs-lookup"><span data-stu-id="f4f87-270">- **True**: Leave the data in the destination object unchanged when you do an upsert/update operation.</span></span> <span data-ttu-id="f4f87-271">Insert a defined default value when you do an insert operation.</span><span class="sxs-lookup"><span data-stu-id="f4f87-271">Insert a defined default value when you do an insert operation.</span></span><br/><span data-ttu-id="f4f87-272">- **False**: Update the data in the destination object to NULL when you do an upsert/update operation.</span><span class="sxs-lookup"><span data-stu-id="f4f87-272">- **False**: Update the data in the destination object to NULL when you do an upsert/update operation.</span></span> <span data-ttu-id="f4f87-273">Insert a NULL value when you do an insert operation.</span><span class="sxs-lookup"><span data-stu-id="f4f87-273">Insert a NULL value when you do an insert operation.</span></span> | <span data-ttu-id="f4f87-274">No (default is false)</span><span class="sxs-lookup"><span data-stu-id="f4f87-274">No (default is false)</span></span> |

>[!NOTE]
><span data-ttu-id="f4f87-275">The default value of the sink "**writeBatchSize**" and the copy activity "**[parallelCopies](copy-activity-performance.md#parallel-copy)**" for the Dynamics sink are both 10.</span><span class="sxs-lookup"><span data-stu-id="f4f87-275">The default value of the sink "**writeBatchSize**" and the copy activity "**[parallelCopies](copy-activity-performance.md#parallel-copy)**" for the Dynamics sink are both 10.</span></span> <span data-ttu-id="f4f87-276">Therefore, 100 records are submitted to Dynamics concurrently.</span><span class="sxs-lookup"><span data-stu-id="f4f87-276">Therefore, 100 records are submitted to Dynamics concurrently.</span></span>

<span data-ttu-id="f4f87-277">For Dynamics 365 online, there is a limit of [2 concurrent batch calls per organization](https://msdn.microsoft.com/en-us/library/jj863631.aspx#Run-time%20limitations).</span><span class="sxs-lookup"><span data-stu-id="f4f87-277">For Dynamics 365 online, there is a limit of [2 concurrent batch calls per organization](https://msdn.microsoft.com/en-us/library/jj863631.aspx#Run-time%20limitations).</span></span> <span data-ttu-id="f4f87-278">If that limit is exceeded, a "Server Busy" fault is thrown before the first request is ever executed.</span><span class="sxs-lookup"><span data-stu-id="f4f87-278">If that limit is exceeded, a "Server Busy" fault is thrown before the first request is ever executed.</span></span> <span data-ttu-id="f4f87-279">Keeping "writeBatchSize" less or equal to 10 would avoid such throttling of concurrent calls.</span><span class="sxs-lookup"><span data-stu-id="f4f87-279">Keeping "writeBatchSize" less or equal to 10 would avoid such throttling of concurrent calls.</span></span>

<span data-ttu-id="f4f87-280">The optimal combination of "**writeBatchSize**" and "**parallelCopies**" depends on the schema of your entity e.g. number of columns, row size, number of plugins/workflows/workflow activities hooked up to those calls, etc. The default setting of 10 writeBatchSize \* 10 parallelCopies is the recommendation according to Dynamics service, which would work for most Dynamics entities though may not be best performance.</span><span class="sxs-lookup"><span data-stu-id="f4f87-280">The optimal combination of "**writeBatchSize**" and "**parallelCopies**" depends on the schema of your entity e.g. number of columns, row size, number of plugins/workflows/workflow activities hooked up to those calls, etc. The default setting of 10 writeBatchSize \* 10 parallelCopies is the recommendation according to Dynamics service, which would work for most Dynamics entities though may not be best performance.</span></span> <span data-ttu-id="f4f87-281">You can tune the performance by adjusting the combination in your copy activity settings.</span><span class="sxs-lookup"><span data-stu-id="f4f87-281">You can tune the performance by adjusting the combination in your copy activity settings.</span></span>

<span data-ttu-id="f4f87-282">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f4f87-282">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyToDynamics",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Dynamics output dataset>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "DynamicsSink",
                "writeBehavior": "Upsert",
                "writeBatchSize": 10,
                "ignoreNullValues": true
            }
        }
    }
]
```

## <a name="data-type-mapping-for-dynamics"></a><span data-ttu-id="f4f87-283">Data type mapping for Dynamics</span><span class="sxs-lookup"><span data-stu-id="f4f87-283">Data type mapping for Dynamics</span></span>

<span data-ttu-id="f4f87-284">When you copy data from Dynamics, the following mappings are used from Dynamics data types to Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="f4f87-284">When you copy data from Dynamics, the following mappings are used from Dynamics data types to Data Factory interim data types.</span></span> <span data-ttu-id="f4f87-285">To learn how the copy activity maps the source schema and data type to the sink, see [Schema and data type mappings](copy-activity-schema-and-type-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="f4f87-285">To learn how the copy activity maps the source schema and data type to the sink, see [Schema and data type mappings](copy-activity-schema-and-type-mapping.md).</span></span>

<span data-ttu-id="f4f87-286">Configure the corresponding Data Factory data type in a dataset structure based on your source Dynamics data type by using the following mapping table.</span><span class="sxs-lookup"><span data-stu-id="f4f87-286">Configure the corresponding Data Factory data type in a dataset structure based on your source Dynamics data type by using the following mapping table.</span></span>

| <span data-ttu-id="f4f87-287">Dynamics data type</span><span class="sxs-lookup"><span data-stu-id="f4f87-287">Dynamics data type</span></span> | <span data-ttu-id="f4f87-288">Data Factory interim data type</span><span class="sxs-lookup"><span data-stu-id="f4f87-288">Data Factory interim data type</span></span> | <span data-ttu-id="f4f87-289">Supported as source</span><span class="sxs-lookup"><span data-stu-id="f4f87-289">Supported as source</span></span> | <span data-ttu-id="f4f87-290">Supported as sink</span><span class="sxs-lookup"><span data-stu-id="f4f87-290">Supported as sink</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f4f87-291">AttributeTypeCode.BigInt</span><span class="sxs-lookup"><span data-stu-id="f4f87-291">AttributeTypeCode.BigInt</span></span> | <span data-ttu-id="f4f87-292">Long</span><span class="sxs-lookup"><span data-stu-id="f4f87-292">Long</span></span> | <span data-ttu-id="f4f87-293">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-293">✓</span></span> | <span data-ttu-id="f4f87-294">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-294">✓</span></span> |
| <span data-ttu-id="f4f87-295">AttributeTypeCode.Boolean</span><span class="sxs-lookup"><span data-stu-id="f4f87-295">AttributeTypeCode.Boolean</span></span> | <span data-ttu-id="f4f87-296">Boolean</span><span class="sxs-lookup"><span data-stu-id="f4f87-296">Boolean</span></span> | <span data-ttu-id="f4f87-297">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-297">✓</span></span> | <span data-ttu-id="f4f87-298">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-298">✓</span></span> |
| <span data-ttu-id="f4f87-299">AttributeType.Customer</span><span class="sxs-lookup"><span data-stu-id="f4f87-299">AttributeType.Customer</span></span> | <span data-ttu-id="f4f87-300">Guid</span><span class="sxs-lookup"><span data-stu-id="f4f87-300">Guid</span></span> | <span data-ttu-id="f4f87-301">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-301">✓</span></span> | | 
| <span data-ttu-id="f4f87-302">AttributeType.DateTime</span><span class="sxs-lookup"><span data-stu-id="f4f87-302">AttributeType.DateTime</span></span> | <span data-ttu-id="f4f87-303">Datetime</span><span class="sxs-lookup"><span data-stu-id="f4f87-303">Datetime</span></span> | <span data-ttu-id="f4f87-304">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-304">✓</span></span> | <span data-ttu-id="f4f87-305">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-305">✓</span></span> |
| <span data-ttu-id="f4f87-306">AttributeType.Decimal</span><span class="sxs-lookup"><span data-stu-id="f4f87-306">AttributeType.Decimal</span></span> | <span data-ttu-id="f4f87-307">Decimal</span><span class="sxs-lookup"><span data-stu-id="f4f87-307">Decimal</span></span> | <span data-ttu-id="f4f87-308">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-308">✓</span></span> | <span data-ttu-id="f4f87-309">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-309">✓</span></span> |
| <span data-ttu-id="f4f87-310">AttributeType.Double</span><span class="sxs-lookup"><span data-stu-id="f4f87-310">AttributeType.Double</span></span> | <span data-ttu-id="f4f87-311">Double</span><span class="sxs-lookup"><span data-stu-id="f4f87-311">Double</span></span> | <span data-ttu-id="f4f87-312">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-312">✓</span></span> | <span data-ttu-id="f4f87-313">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-313">✓</span></span> |
| <span data-ttu-id="f4f87-314">AttributeType.EntityName</span><span class="sxs-lookup"><span data-stu-id="f4f87-314">AttributeType.EntityName</span></span> | <span data-ttu-id="f4f87-315">String</span><span class="sxs-lookup"><span data-stu-id="f4f87-315">String</span></span> | <span data-ttu-id="f4f87-316">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-316">✓</span></span> | <span data-ttu-id="f4f87-317">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-317">✓</span></span> |
| <span data-ttu-id="f4f87-318">AttributeType.Integer</span><span class="sxs-lookup"><span data-stu-id="f4f87-318">AttributeType.Integer</span></span> | <span data-ttu-id="f4f87-319">Int32</span><span class="sxs-lookup"><span data-stu-id="f4f87-319">Int32</span></span> | <span data-ttu-id="f4f87-320">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-320">✓</span></span> | <span data-ttu-id="f4f87-321">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-321">✓</span></span> |
| <span data-ttu-id="f4f87-322">AttributeType.Lookup</span><span class="sxs-lookup"><span data-stu-id="f4f87-322">AttributeType.Lookup</span></span> | <span data-ttu-id="f4f87-323">Guid</span><span class="sxs-lookup"><span data-stu-id="f4f87-323">Guid</span></span> | <span data-ttu-id="f4f87-324">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-324">✓</span></span> | <span data-ttu-id="f4f87-325">✓ (with single target associated)</span><span class="sxs-lookup"><span data-stu-id="f4f87-325">✓ (with single target associated)</span></span> |
| <span data-ttu-id="f4f87-326">AttributeType.ManagedProperty</span><span class="sxs-lookup"><span data-stu-id="f4f87-326">AttributeType.ManagedProperty</span></span> | <span data-ttu-id="f4f87-327">Boolean</span><span class="sxs-lookup"><span data-stu-id="f4f87-327">Boolean</span></span> | <span data-ttu-id="f4f87-328">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-328">✓</span></span> | |
| <span data-ttu-id="f4f87-329">AttributeType.Memo</span><span class="sxs-lookup"><span data-stu-id="f4f87-329">AttributeType.Memo</span></span> | <span data-ttu-id="f4f87-330">String</span><span class="sxs-lookup"><span data-stu-id="f4f87-330">String</span></span> | <span data-ttu-id="f4f87-331">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-331">✓</span></span> | <span data-ttu-id="f4f87-332">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-332">✓</span></span> |
| <span data-ttu-id="f4f87-333">AttributeType.Money</span><span class="sxs-lookup"><span data-stu-id="f4f87-333">AttributeType.Money</span></span> | <span data-ttu-id="f4f87-334">Decimal</span><span class="sxs-lookup"><span data-stu-id="f4f87-334">Decimal</span></span> | <span data-ttu-id="f4f87-335">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-335">✓</span></span> | <span data-ttu-id="f4f87-336">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-336">✓</span></span> |
| <span data-ttu-id="f4f87-337">AttributeType.Owner</span><span class="sxs-lookup"><span data-stu-id="f4f87-337">AttributeType.Owner</span></span> | <span data-ttu-id="f4f87-338">Guid</span><span class="sxs-lookup"><span data-stu-id="f4f87-338">Guid</span></span> | <span data-ttu-id="f4f87-339">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-339">✓</span></span> | |
| <span data-ttu-id="f4f87-340">AttributeType.Picklist</span><span class="sxs-lookup"><span data-stu-id="f4f87-340">AttributeType.Picklist</span></span> | <span data-ttu-id="f4f87-341">Int32</span><span class="sxs-lookup"><span data-stu-id="f4f87-341">Int32</span></span> | <span data-ttu-id="f4f87-342">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-342">✓</span></span> | <span data-ttu-id="f4f87-343">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-343">✓</span></span> |
| <span data-ttu-id="f4f87-344">AttributeType.Uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="f4f87-344">AttributeType.Uniqueidentifier</span></span> | <span data-ttu-id="f4f87-345">Guid</span><span class="sxs-lookup"><span data-stu-id="f4f87-345">Guid</span></span> | <span data-ttu-id="f4f87-346">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-346">✓</span></span> | <span data-ttu-id="f4f87-347">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-347">✓</span></span> |
| <span data-ttu-id="f4f87-348">AttributeType.String</span><span class="sxs-lookup"><span data-stu-id="f4f87-348">AttributeType.String</span></span> | <span data-ttu-id="f4f87-349">String</span><span class="sxs-lookup"><span data-stu-id="f4f87-349">String</span></span> | <span data-ttu-id="f4f87-350">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-350">✓</span></span> | <span data-ttu-id="f4f87-351">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-351">✓</span></span> |
| <span data-ttu-id="f4f87-352">AttributeType.State</span><span class="sxs-lookup"><span data-stu-id="f4f87-352">AttributeType.State</span></span> | <span data-ttu-id="f4f87-353">Int32</span><span class="sxs-lookup"><span data-stu-id="f4f87-353">Int32</span></span> | <span data-ttu-id="f4f87-354">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-354">✓</span></span> | <span data-ttu-id="f4f87-355">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-355">✓</span></span> |
| <span data-ttu-id="f4f87-356">AttributeType.Status</span><span class="sxs-lookup"><span data-stu-id="f4f87-356">AttributeType.Status</span></span> | <span data-ttu-id="f4f87-357">Int32</span><span class="sxs-lookup"><span data-stu-id="f4f87-357">Int32</span></span> | <span data-ttu-id="f4f87-358">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-358">✓</span></span> | <span data-ttu-id="f4f87-359">✓</span><span class="sxs-lookup"><span data-stu-id="f4f87-359">✓</span></span> |


> [!NOTE]
> <span data-ttu-id="f4f87-360">The Dynamics data types AttributeType.CalendarRules and AttributeType.PartyList aren't supported.</span><span class="sxs-lookup"><span data-stu-id="f4f87-360">The Dynamics data types AttributeType.CalendarRules and AttributeType.PartyList aren't supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4f87-361">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4f87-361">Next steps</span></span>
<span data-ttu-id="f4f87-362">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f4f87-362">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
