---
title: Configure Azure Application Insights smart detection rule settings with Azure Resource Manager templates | Microsoft Docs
description: Automate management and configuration of Azure Application Insights smart detection rules with Azure Resource Manager Templates
services: application-insights
documentationcenter: ''
author: harelbr
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 07/19/2018
ms.reviewer: mbullwin
ms.author: harelbr
ms.openlocfilehash: 79c4746916c4da39c3aed9df978ca1c3bd9ff5d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856219"
---
# <a name="manage-application-insights-smart-detection-rules-using-azure-resource-manager-templates"></a><span data-ttu-id="ff98b-103">Manage Application Insights smart detection rules using Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="ff98b-103">Manage Application Insights smart detection rules using Azure Resource Manager templates</span></span>

<span data-ttu-id="ff98b-104">Smart detection rules in Application Insights can be managed and configured using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ff98b-104">Smart detection rules in Application Insights can be managed and configured using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
<span data-ttu-id="ff98b-105">This method can be used when deploying new Application Insights resources with Azure Resource Manager automation, or for modifying the settings of existing resources.</span><span class="sxs-lookup"><span data-stu-id="ff98b-105">This method can be used when deploying new Application Insights resources with Azure Resource Manager automation, or for modifying the settings of existing resources.</span></span>

## <a name="smart-detection-rule-configuration"></a><span data-ttu-id="ff98b-106">Smart detection rule configuration</span><span class="sxs-lookup"><span data-stu-id="ff98b-106">Smart detection rule configuration</span></span>

<span data-ttu-id="ff98b-107">You can configure the following settings for a smart detection rule:</span><span class="sxs-lookup"><span data-stu-id="ff98b-107">You can configure the following settings for a smart detection rule:</span></span>
- <span data-ttu-id="ff98b-108">If the rule is enabled (the default is **true**.)</span><span class="sxs-lookup"><span data-stu-id="ff98b-108">If the rule is enabled (the default is **true**.)</span></span>
- <span data-ttu-id="ff98b-109">If emails should be sent to the subscription owners, contributors and readers when a detection is found (the default is **true**.)</span><span class="sxs-lookup"><span data-stu-id="ff98b-109">If emails should be sent to the subscription owners, contributors and readers when a detection is found (the default is **true**.)</span></span>
- <span data-ttu-id="ff98b-110">Any additional email recipients who should get a notification when a detection is found.</span><span class="sxs-lookup"><span data-stu-id="ff98b-110">Any additional email recipients who should get a notification when a detection is found.</span></span>

<span data-ttu-id="ff98b-111">To allow configuring the rule settings via Azure Resource Manager, the smart detection rule configuration is now available as an inner resource within the Application Insights resource, named **ProactiveDetectionConfigs**.</span><span class="sxs-lookup"><span data-stu-id="ff98b-111">To allow configuring the rule settings via Azure Resource Manager, the smart detection rule configuration is now available as an inner resource within the Application Insights resource, named **ProactiveDetectionConfigs**.</span></span>
<span data-ttu-id="ff98b-112">For maximal flexibility, each smart detection rule can be configured with unique notification settings.</span><span class="sxs-lookup"><span data-stu-id="ff98b-112">For maximal flexibility, each smart detection rule can be configured with unique notification settings.</span></span>

## <a name="examples"></a><span data-ttu-id="ff98b-113">Examples</span><span class="sxs-lookup"><span data-stu-id="ff98b-113">Examples</span></span>

<span data-ttu-id="ff98b-114">Below are a few examples showing how to configure the settings of smart detection rules using Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="ff98b-114">Below are a few examples showing how to configure the settings of smart detection rules using Azure Resource Manager templates.</span></span>
<span data-ttu-id="ff98b-115">All samples refer to an Application Insights resource named _“myApplication”_, and to the "long dependency duration smart detection rule", which is internally named _“longdependencyduration”_.</span><span class="sxs-lookup"><span data-stu-id="ff98b-115">All samples refer to an Application Insights resource named _“myApplication”_, and to the "long dependency duration smart detection rule", which is internally named _“longdependencyduration”_.</span></span>
<span data-ttu-id="ff98b-116">Make sure to replace the Application Insights resource name, and to specify the relevant smart detection rule internal name.</span><span class="sxs-lookup"><span data-stu-id="ff98b-116">Make sure to replace the Application Insights resource name, and to specify the relevant smart detection rule internal name.</span></span> <span data-ttu-id="ff98b-117">Check the table below for a list of the corresponding internal Azure Resource Manager names for each smart detection rule.</span><span class="sxs-lookup"><span data-stu-id="ff98b-117">Check the table below for a list of the corresponding internal Azure Resource Manager names for each smart detection rule.</span></span>

### <a name="disable-a-smart-detection-rule"></a><span data-ttu-id="ff98b-118">Disable a smart detection rule</span><span class="sxs-lookup"><span data-stu-id="ff98b-118">Disable a smart detection rule</span></span>

```json
{
      "apiVersion": "2018-05-01-preview",
      "name": "myApplication",
      "type": "Microsoft.Insights/components",
      "location": "[resourceGroup().location]",
      "properties": {
        "ApplicationId": "myApplication"
      },
      "resources": [
        {
          "apiVersion": "2018-05-01-preview",
          "name": "longdependencyduration",
          "type": "ProactiveDetectionConfigs",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Insights/components', 'myApplication')]"
          ],
          "properties": {
            "name": "longdependencyduration",
            "sendEmailsToSubscriptionOwners": true,
            "customEmails": [],
            "enabled": false
          }
        }
      ]
    }
```

### <a name="disable-sending-email-notifications-for-a-smart-detection-rule"></a><span data-ttu-id="ff98b-119">Disable sending email notifications for a smart detection rule</span><span class="sxs-lookup"><span data-stu-id="ff98b-119">Disable sending email notifications for a smart detection rule</span></span>

```json
{
      "apiVersion": "2018-05-01-preview",
      "name": "myApplication",
      "type": "Microsoft.Insights/components",
      "location": "[resourceGroup().location]",
      "properties": {
        "ApplicationId": "myApplication"
      },
      "resources": [
        {
          "apiVersion": "2018-05-01-preview",
          "name": "longdependencyduration",
          "type": "ProactiveDetectionConfigs",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Insights/components', 'myApplication')]"
          ],
          "properties": {
            "name": "longdependencyduration",
            "sendEmailsToSubscriptionOwners": false,
            "customEmails": [],
            "enabled": true
          }
        }
      ]
    }
```

### <a name="add-additional-email-recipients-for-a-smart-detection-rule"></a><span data-ttu-id="ff98b-120">Add additional email recipients for a smart detection rule</span><span class="sxs-lookup"><span data-stu-id="ff98b-120">Add additional email recipients for a smart detection rule</span></span>

```json
{
      "apiVersion": "2018-05-01-preview",
      "name": "myApplication",
      "type": "Microsoft.Insights/components",
      "location": "[resourceGroup().location]",
      "properties": {
        "ApplicationId": "myApplication"
      },
      "resources": [
        {
          "apiVersion": "2018-05-01-preview",
          "name": "longdependencyduration",
          "type": "ProactiveDetectionConfigs",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Insights/components', 'myApplication')]"
          ],
          "properties": {
            "name": "longdependencyduration",
            "sendEmailsToSubscriptionOwners": true,
            "customEmails": ['alice@contoso.com', 'bob@contoso.com'],
            "enabled": true
          }
        }
      ]
    }

```

## <a name="smart-detection-rule-names"></a><span data-ttu-id="ff98b-121">Smart detection rule names</span><span class="sxs-lookup"><span data-stu-id="ff98b-121">Smart detection rule names</span></span>

<span data-ttu-id="ff98b-122">Below is a table of smart detection rule names as they appear in the portal, along with their internal names, that should be used in the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="ff98b-122">Below is a table of smart detection rule names as they appear in the portal, along with their internal names, that should be used in the Azure Resource Manager template.</span></span>

> [!NOTE]
> <span data-ttu-id="ff98b-123">Smart detection rules marked as preview don’t support email notifications.</span><span class="sxs-lookup"><span data-stu-id="ff98b-123">Smart detection rules marked as preview don’t support email notifications.</span></span> <span data-ttu-id="ff98b-124">Therefore, you can only set the enabled property for these rules.</span><span class="sxs-lookup"><span data-stu-id="ff98b-124">Therefore, you can only set the enabled property for these rules.</span></span> 

| <span data-ttu-id="ff98b-125">Azure portal rule name</span><span class="sxs-lookup"><span data-stu-id="ff98b-125">Azure portal rule name</span></span> | <span data-ttu-id="ff98b-126">Internal name</span><span class="sxs-lookup"><span data-stu-id="ff98b-126">Internal name</span></span>
|:---|:---|
| <span data-ttu-id="ff98b-127">Slow page load time</span><span class="sxs-lookup"><span data-stu-id="ff98b-127">Slow page load time</span></span> | <span data-ttu-id="ff98b-128">slowpageloadtime</span><span class="sxs-lookup"><span data-stu-id="ff98b-128">slowpageloadtime</span></span> |
| <span data-ttu-id="ff98b-129">Slow server response time</span><span class="sxs-lookup"><span data-stu-id="ff98b-129">Slow server response time</span></span> | <span data-ttu-id="ff98b-130">slowserverresponsetime</span><span class="sxs-lookup"><span data-stu-id="ff98b-130">slowserverresponsetime</span></span> |
| <span data-ttu-id="ff98b-131">Long dependency duration</span><span class="sxs-lookup"><span data-stu-id="ff98b-131">Long dependency duration</span></span> | <span data-ttu-id="ff98b-132">longdependencyduration</span><span class="sxs-lookup"><span data-stu-id="ff98b-132">longdependencyduration</span></span> |
| <span data-ttu-id="ff98b-133">Degradation in server response time</span><span class="sxs-lookup"><span data-stu-id="ff98b-133">Degradation in server response time</span></span> | <span data-ttu-id="ff98b-134">degradationinserverresponsetime</span><span class="sxs-lookup"><span data-stu-id="ff98b-134">degradationinserverresponsetime</span></span> |
| <span data-ttu-id="ff98b-135">Degradation in dependency duration</span><span class="sxs-lookup"><span data-stu-id="ff98b-135">Degradation in dependency duration</span></span> | <span data-ttu-id="ff98b-136">degradationindependencyduration</span><span class="sxs-lookup"><span data-stu-id="ff98b-136">degradationindependencyduration</span></span> |
| <span data-ttu-id="ff98b-137">Degradation in trace severity ratio (preview)</span><span class="sxs-lookup"><span data-stu-id="ff98b-137">Degradation in trace severity ratio (preview)</span></span> | <span data-ttu-id="ff98b-138">extension_traceseveritydetector</span><span class="sxs-lookup"><span data-stu-id="ff98b-138">extension_traceseveritydetector</span></span> |
| <span data-ttu-id="ff98b-139">Abnormal rise in exception volume (preview)</span><span class="sxs-lookup"><span data-stu-id="ff98b-139">Abnormal rise in exception volume (preview)</span></span> | <span data-ttu-id="ff98b-140">extension_exceptionchangeextension</span><span class="sxs-lookup"><span data-stu-id="ff98b-140">extension_exceptionchangeextension</span></span> |
| <span data-ttu-id="ff98b-141">Potential memory leak detected (preview)</span><span class="sxs-lookup"><span data-stu-id="ff98b-141">Potential memory leak detected (preview)</span></span> | <span data-ttu-id="ff98b-142">extension_memoryleakextension</span><span class="sxs-lookup"><span data-stu-id="ff98b-142">extension_memoryleakextension</span></span> |
| <span data-ttu-id="ff98b-143">Potential security issue detected (preview)</span><span class="sxs-lookup"><span data-stu-id="ff98b-143">Potential security issue detected (preview)</span></span> | <span data-ttu-id="ff98b-144">extension_securityextensionspackage</span><span class="sxs-lookup"><span data-stu-id="ff98b-144">extension_securityextensionspackage</span></span> |
| <span data-ttu-id="ff98b-145">Resource utilization issue detected (preview)</span><span class="sxs-lookup"><span data-stu-id="ff98b-145">Resource utilization issue detected (preview)</span></span> | <span data-ttu-id="ff98b-146">extension_resourceutilizationextensionspackage</span><span class="sxs-lookup"><span data-stu-id="ff98b-146">extension_resourceutilizationextensionspackage</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ff98b-147">Next Steps</span><span class="sxs-lookup"><span data-stu-id="ff98b-147">Next Steps</span></span>

<span data-ttu-id="ff98b-148">Learn more about automatically detecting:</span><span class="sxs-lookup"><span data-stu-id="ff98b-148">Learn more about automatically detecting:</span></span>

- [<span data-ttu-id="ff98b-149">Failure anomalies</span><span class="sxs-lookup"><span data-stu-id="ff98b-149">Failure anomalies</span></span>](app-insights-proactive-failure-diagnostics.md)
- [<span data-ttu-id="ff98b-150">Memory Leaks</span><span class="sxs-lookup"><span data-stu-id="ff98b-150">Memory Leaks</span></span>](app-insights-proactive-potential-memory-leak.md)
- [<span data-ttu-id="ff98b-151">Performance anomalies</span><span class="sxs-lookup"><span data-stu-id="ff98b-151">Performance anomalies</span></span>](app-insights-proactive-performance-diagnostics.md)