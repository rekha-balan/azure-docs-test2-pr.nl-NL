---
title: Automate Azure Application Insights with PowerShell | Microsoft Docs
description: Automate creating resource, alert, and availability tests in PowerShell using an Azure Resource Manager template.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 9f73b87f-be63-4847-88c8-368543acad8b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: awills
ms.openlocfilehash: 1ef6ac1f52cd153c2d99420e0d8c65f8806d0789
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549271"
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="38f06-103">Create Application Insights resources using PowerShell</span><span class="sxs-lookup"><span data-stu-id="38f06-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="38f06-104">This article shows you how to automate the creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span><span class="sxs-lookup"><span data-stu-id="38f06-104">This article shows you how to automate the creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="38f06-105">You might, for example, do so as part of a build process.</span><span class="sxs-lookup"><span data-stu-id="38f06-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="38f06-106">Along with the basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set the [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="38f06-106">Along with the basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set the [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="38f06-107">The key to creating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="38f06-107">The key to creating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="38f06-108">In a nutshell, the procedure is: download the JSON definitions of existing resources; parameterize certain values such as names; and then run the template whenever you want to create a new resource.</span><span class="sxs-lookup"><span data-stu-id="38f06-108">In a nutshell, the procedure is: download the JSON definitions of existing resources; parameterize certain values such as names; and then run the template whenever you want to create a new resource.</span></span> <span data-ttu-id="38f06-109">You can package several resources together, to create them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span><span class="sxs-lookup"><span data-stu-id="38f06-109">You can package several resources together, to create them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="38f06-110">There are some subtleties to some of the parameterizations, which we'll explain here.</span><span class="sxs-lookup"><span data-stu-id="38f06-110">There are some subtleties to some of the parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="38f06-111">One-time setup</span><span class="sxs-lookup"><span data-stu-id="38f06-111">One-time setup</span></span>
<span data-ttu-id="38f06-112">If you haven't used PowerShell with your Azure subscription before:</span><span class="sxs-lookup"><span data-stu-id="38f06-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="38f06-113">Install the Azure Powershell module on the machine where you want to run the scripts:</span><span class="sxs-lookup"><span data-stu-id="38f06-113">Install the Azure Powershell module on the machine where you want to run the scripts:</span></span>

1. <span data-ttu-id="38f06-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="38f06-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="38f06-115">Use it to install Microsoft Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="38f06-115">Use it to install Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="38f06-116">Create an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="38f06-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="38f06-117">Create a new .json file - let's call it `template1.json` in this example.</span><span class="sxs-lookup"><span data-stu-id="38f06-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="38f06-118">Copy this content into it:</span><span class="sxs-lookup"><span data-stu-id="38f06-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter the application name."
                }
            },
            "appType": {
                "type": "string",
                "defaultValue": "web",
                "allowedValues": [
                    "web",
                    "java",
                    "HockeyAppBridge",
                    "other"
                ],
                "metadata": {
                    "description": "Enter the application type."
                }
            },
            "appLocation": {
                "type": "string",
                "defaultValue": "East US",
                "allowedValues": [
                    "South Central US",
                    "West Europe",
                    "East US",
                    "North Europe"
                ],
                "metadata": {
                    "description": "Enter the application location."
                }
            },
            "priceCode": {
                "type": "int",
                "defaultValue": 1,
                "allowedValues": [
                    1,
                    2
                ],
                "metadata": {
                    "description": "1 = Basic, 2 = Enterprise"
                }
            },
            "dailyQuota": {
                "type": "int",
                "defaultValue": 100,
                "minValue": 1,
                "metadata": {
                    "description": "Enter daily quota in GB."
                }
            },
            "dailyQuotaResetTime": {
                "type": "int",
                "defaultValue": 24,
                "metadata": {
                    "description": "Enter daily quota reset hour in UTC (0 to 23). Values outside the range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter the % value of daily quota after which warning mail to be sent. "
                }
            }
        },
        "variables": {
            "priceArray": [
                "Basic",
                "Application Insights Enterprise"
            ],
            "pricePlan": "[take(variables('priceArray'),parameters('priceCode'))]",
            "billingplan": "[concat(parameters('appName'),'/', variables('pricePlan')[0])]"
        },
        "resources": [
            {
                "type": "microsoft.insights/components",
                "kind": "[parameters('appType')]",
                "name": "[parameters('appName')]",
                "apiVersion": "2014-04-01",
                "location": "[parameters('appLocation')]",
                "tags": {},
                "properties": {
                    "ApplicationId": "[parameters('appName')]"
                },
                "dependsOn": []
            },
            {
                "name": "[variables('billingplan')]",
                "type": "microsoft.insights/components/CurrentBillingFeatures",
                "location": "[parameters('appLocation')]",
                "apiVersion": "2015-05-01",
                "dependsOn": [
                    "[resourceId('microsoft.insights/components', parameters('appName'))]"
                ],
                "properties": {
                    "CurrentBillingFeatures": "[variables('pricePlan')]",
                    "DataVolumeCap": {
                        "Cap": "[parameters('dailyQuota')]",
                        "WarningThreshold": "[parameters('warningThreshold')]",
                        "ResetTime": "[parameters('dailyQuotaResetTime')]"
                    }
                }
            }
        ]
    }
```



## <a name="create-application-insights-resources"></a><span data-ttu-id="38f06-119">Create Application Insights resources</span><span class="sxs-lookup"><span data-stu-id="38f06-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="38f06-120">In PowerShell, sign in to Azure:</span><span class="sxs-lookup"><span data-stu-id="38f06-120">In PowerShell, sign in to Azure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="38f06-121">Run a command like this:</span><span class="sxs-lookup"><span data-stu-id="38f06-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="38f06-122">`-ResourceGroupName` is the group where you want to create the new resources.</span><span class="sxs-lookup"><span data-stu-id="38f06-122">`-ResourceGroupName` is the group where you want to create the new resources.</span></span>
   * <span data-ttu-id="38f06-123">`-TemplateFile` must occur before the custom parameters.</span><span class="sxs-lookup"><span data-stu-id="38f06-123">`-TemplateFile` must occur before the custom parameters.</span></span>
   * <span data-ttu-id="38f06-124">`-appName` The name of the resource to create.</span><span class="sxs-lookup"><span data-stu-id="38f06-124">`-appName` The name of the resource to create.</span></span>

<span data-ttu-id="38f06-125">You can add other parameters - you'll find their descriptions in the parameters section of the template.</span><span class="sxs-lookup"><span data-stu-id="38f06-125">You can add other parameters - you'll find their descriptions in the parameters section of the template.</span></span>

## <a name="to-get-the-instrumentation-key"></a><span data-ttu-id="38f06-126">To get the instrumentation key</span><span class="sxs-lookup"><span data-stu-id="38f06-126">To get the instrumentation key</span></span>
<span data-ttu-id="38f06-127">After creating an application resource, you'll want the instrumentation key:</span><span class="sxs-lookup"><span data-stu-id="38f06-127">After creating an application resource, you'll want the instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-the-price-plan"></a><span data-ttu-id="38f06-128">Set the price plan</span><span class="sxs-lookup"><span data-stu-id="38f06-128">Set the price plan</span></span>

<span data-ttu-id="38f06-129">You can set the [price plan](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="38f06-129">You can set the [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="38f06-130">To create an app resource with the Enterprise price plan, using the template above:</span><span class="sxs-lookup"><span data-stu-id="38f06-130">To create an app resource with the Enterprise price plan, using the template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="38f06-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="38f06-131">priceCode</span></span>|<span data-ttu-id="38f06-132">plan</span><span class="sxs-lookup"><span data-stu-id="38f06-132">plan</span></span>|
|---|---|
|<span data-ttu-id="38f06-133">1</span><span class="sxs-lookup"><span data-stu-id="38f06-133">1</span></span>|<span data-ttu-id="38f06-134">Basic</span><span class="sxs-lookup"><span data-stu-id="38f06-134">Basic</span></span>|
|<span data-ttu-id="38f06-135">2</span><span class="sxs-lookup"><span data-stu-id="38f06-135">2</span></span>|<span data-ttu-id="38f06-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="38f06-136">Enterprise</span></span>|

* <span data-ttu-id="38f06-137">If you only want to use the default Basic price plan, you can omit the CurrentBillingFeatures resource from the template.</span><span class="sxs-lookup"><span data-stu-id="38f06-137">If you only want to use the default Basic price plan, you can omit the CurrentBillingFeatures resource from the template.</span></span>
* <span data-ttu-id="38f06-138">If you want to change the price plan after the component resource has been created, you can use a template that omits the "microsoft.insights/components" resource.</span><span class="sxs-lookup"><span data-stu-id="38f06-138">If you want to change the price plan after the component resource has been created, you can use a template that omits the "microsoft.insights/components" resource.</span></span> <span data-ttu-id="38f06-139">Also, omit the `dependsOn` node from the billing resource.</span><span class="sxs-lookup"><span data-stu-id="38f06-139">Also, omit the `dependsOn` node from the billing resource.</span></span> 

<span data-ttu-id="38f06-140">To verify the updated price plan, look at the "Features+pricing" blade in the browser.</span><span class="sxs-lookup"><span data-stu-id="38f06-140">To verify the updated price plan, look at the "Features+pricing" blade in the browser.</span></span> <span data-ttu-id="38f06-141">**Refresh the browser view** to make sure you see the latest state.</span><span class="sxs-lookup"><span data-stu-id="38f06-141">**Refresh the browser view** to make sure you see the latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="38f06-142">Add a metric alert</span><span class="sxs-lookup"><span data-stu-id="38f06-142">Add a metric alert</span></span>

<span data-ttu-id="38f06-143">To set up a metric alert at the same time as your app resource, merge code like this into the template file:</span><span class="sxs-lookup"><span data-stu-id="38f06-143">To set up a metric alert at the same time as your app resource, merge code like this into the template file:</span></span>

```JSON
{
    parameters: { ... // existing parameters ...
            "responseTime": {
              "type": "int",
              "defaultValue": 3,
              "minValue": 1,
              "metadata": {
                "description": "Enter response time threshold in seconds."
              }
    },
    variables: { ... // existing variables ...
      // Alert names must be unique within resource group.
      "responseAlertName": "[concat('ResponseTime-', toLower(parameters('appName')))]"
    }, 
    resources: { ... // existing resources ...
     {
      //
      // Metric alert on response time
      //
      "name": "[variables('responseAlertName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this resource is created after the app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('responseAlertName')]",
        "description": "response time alert",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/components', parameters('appName'))]",
            "metricName": "request.duration"
          },
          "threshold": "[parameters('responseTime')]", //seconds
          "windowSize": "PT15M" // Take action if changed state for 15 minutes
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="38f06-144">When you invoke the template, you can optionally add this parameter:</span><span class="sxs-lookup"><span data-stu-id="38f06-144">When you invoke the template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="38f06-145">You can of course parameterize other fields.</span><span class="sxs-lookup"><span data-stu-id="38f06-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="38f06-146">To find out the type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="38f06-146">To find out the type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="38f06-147">Add an availability test</span><span class="sxs-lookup"><span data-stu-id="38f06-147">Add an availability test</span></span>

<span data-ttu-id="38f06-148">This example is for a ping test (to test a single page).</span><span class="sxs-lookup"><span data-stu-id="38f06-148">This example is for a ping test (to test a single page).</span></span>  

<span data-ttu-id="38f06-149">**There are two parts** in an availability test: the test itself, and the alert that notifies you of failures.</span><span class="sxs-lookup"><span data-stu-id="38f06-149">**There are two parts** in an availability test: the test itself, and the alert that notifies you of failures.</span></span>

<span data-ttu-id="38f06-150">Merge the following code into the template file that creates the app.</span><span class="sxs-lookup"><span data-stu-id="38f06-150">Merge the following code into the template file that creates the app.</span></span>

```JSON
{
    parameters: { ... // existing parameters here ...
      "pingURL": { "type": "string" },
      "pingText": { "type": "string" , defaultValue: ""}
    },
    variables: { ... // existing variables here ...
      "pingTestName":"[concat('PingTest-', toLower(parameters('appName')))]",
      "pingAlertRuleName": "[concat('PingAlert-', toLower(parameters('appName')), '-', subscription().subscriptionId)]"
    },
    resources: { ... // existing resources here ...
    { //
      // Availability test: part 1 configures the test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after the app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "Name": "[variables('pingTestName')]",
        "Description": "Basic ping test",
        "Enabled": true,
        "Frequency": 900, // 15 minutes
        "Timeout": 120, // 2 minutes
        "Kind": "ping", // single URL test
        "RetryEnabled": true,
        "Locations": [
          {
            "Id": "us-va-ash-azr"
          },
          {
            "Id": "emea-nl-ams-azr"
          },
          {
            "Id": "apac-jp-kaw-edge"
          }
        ],
        "Configuration": {
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies the existence of the specified text in the response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, the alert rule
      //
      "name": "[variables('pingAlertRuleName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]", 
      "dependsOn": [
        "[resourceId('Microsoft.Insights/webtests', variables('pingTestName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource",
        "[concat('hidden-link:', resourceId('Microsoft.Insights/webtests', variables('pingTestName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('pingAlertRuleName')]",
        "description": "alert for web test",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.LocationThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.LocationThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/webtests', variables('pingTestName'))]",
            "metricName": "GSMT_AvRaW"
          },
          "windowSize": "PT15M", // Take action if changed state for 15 minutes
          "failedLocationCount": 2
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="38f06-151">To discover the codes for other test locations, or to automate the creation of more complex web tests, create an example manually and then parameterize the code from [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="38f06-151">To discover the codes for other test locations, or to automate the creation of more complex web tests, create an example manually and then parameterize the code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="38f06-152">Add more resources</span><span class="sxs-lookup"><span data-stu-id="38f06-152">Add more resources</span></span>

<span data-ttu-id="38f06-153">To automate the creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="38f06-153">To automate the creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="38f06-154">Open [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="38f06-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="38f06-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, to your application resource.</span><span class="sxs-lookup"><span data-stu-id="38f06-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, to your application resource.</span></span> 
   
    ![Navigation in Azure Resource Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-powershell/01.png)
   
    <span data-ttu-id="38f06-157">*Components* are the basic Application Insights resources for displaying applications.</span><span class="sxs-lookup"><span data-stu-id="38f06-157">*Components* are the basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="38f06-158">There are separate resources for the associated alert rules and availability web tests.</span><span class="sxs-lookup"><span data-stu-id="38f06-158">There are separate resources for the associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="38f06-159">Copy the JSON of the component into the appropriate place in `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="38f06-159">Copy the JSON of the component into the appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="38f06-160">Delete these properties:</span><span class="sxs-lookup"><span data-stu-id="38f06-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="38f06-161">Open the webtests and alertrules sections and copy the JSON for individual items into your template.</span><span class="sxs-lookup"><span data-stu-id="38f06-161">Open the webtests and alertrules sections and copy the JSON for individual items into your template.</span></span> <span data-ttu-id="38f06-162">(Don't copy from the webtests or alertrules nodes: go into the items under them.)</span><span class="sxs-lookup"><span data-stu-id="38f06-162">(Don't copy from the webtests or alertrules nodes: go into the items under them.)</span></span>
   
    <span data-ttu-id="38f06-163">Each web test has an associated alert rule, so you have to copy both of them.</span><span class="sxs-lookup"><span data-stu-id="38f06-163">Each web test has an associated alert rule, so you have to copy both of them.</span></span>
   
    <span data-ttu-id="38f06-164">You can also include alerts on metrics.</span><span class="sxs-lookup"><span data-stu-id="38f06-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="38f06-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="38f06-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="38f06-166">Insert this line in each resource:</span><span class="sxs-lookup"><span data-stu-id="38f06-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-the-template"></a><span data-ttu-id="38f06-167">Parameterize the template</span><span class="sxs-lookup"><span data-stu-id="38f06-167">Parameterize the template</span></span>
<span data-ttu-id="38f06-168">Now you have to replace the specific names with parameters.</span><span class="sxs-lookup"><span data-stu-id="38f06-168">Now you have to replace the specific names with parameters.</span></span> <span data-ttu-id="38f06-169">To [parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="38f06-169">To [parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="38f06-170">You can't parameterize just part of a string, so use `concat()` to build strings.</span><span class="sxs-lookup"><span data-stu-id="38f06-170">You can't parameterize just part of a string, so use `concat()` to build strings.</span></span>

<span data-ttu-id="38f06-171">Here are examples of the substitutions you'll want to make.</span><span class="sxs-lookup"><span data-stu-id="38f06-171">Here are examples of the substitutions you'll want to make.</span></span> <span data-ttu-id="38f06-172">There are several occurrences of each substitution.</span><span class="sxs-lookup"><span data-stu-id="38f06-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="38f06-173">You might need others in your template.</span><span class="sxs-lookup"><span data-stu-id="38f06-173">You might need others in your template.</span></span> <span data-ttu-id="38f06-174">These examples use the parameters and variables we defined at the top of the template.</span><span class="sxs-lookup"><span data-stu-id="38f06-174">These examples use the parameters and variables we defined at the top of the template.</span></span>

| <span data-ttu-id="38f06-175">find</span><span class="sxs-lookup"><span data-stu-id="38f06-175">find</span></span> | <span data-ttu-id="38f06-176">replace with</span><span class="sxs-lookup"><span data-stu-id="38f06-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="38f06-177">`"myappname"` (lower case)</span><span class="sxs-lookup"><span data-stu-id="38f06-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="38f06-178">Delete Guid and Id.</span><span class="sxs-lookup"><span data-stu-id="38f06-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-the-resources"></a><span data-ttu-id="38f06-179">Set dependencies between the resources</span><span class="sxs-lookup"><span data-stu-id="38f06-179">Set dependencies between the resources</span></span>
<span data-ttu-id="38f06-180">Azure should set up the resources in strict order.</span><span class="sxs-lookup"><span data-stu-id="38f06-180">Azure should set up the resources in strict order.</span></span> <span data-ttu-id="38f06-181">To make sure one setup completes before the next begins, add dependency lines:</span><span class="sxs-lookup"><span data-stu-id="38f06-181">To make sure one setup completes before the next begins, add dependency lines:</span></span>

* <span data-ttu-id="38f06-182">In the availability test resource:</span><span class="sxs-lookup"><span data-stu-id="38f06-182">In the availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="38f06-183">In the alert resource for an availability test:</span><span class="sxs-lookup"><span data-stu-id="38f06-183">In the alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="38f06-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="38f06-184">Next steps</span></span>
<span data-ttu-id="38f06-185">Other automation articles:</span><span class="sxs-lookup"><span data-stu-id="38f06-185">Other automation articles:</span></span>

* <span data-ttu-id="38f06-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span><span class="sxs-lookup"><span data-stu-id="38f06-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="38f06-187">Set up Alerts</span><span class="sxs-lookup"><span data-stu-id="38f06-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="38f06-188">Create web tests</span><span class="sxs-lookup"><span data-stu-id="38f06-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="38f06-189">Send Azure Diagnostics to Application Insights</span><span class="sxs-lookup"><span data-stu-id="38f06-189">Send Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="38f06-190">Deploy to Azure from GitHub</span><span class="sxs-lookup"><span data-stu-id="38f06-190">Deploy to Azure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="38f06-191">Create release annotations</span><span class="sxs-lookup"><span data-stu-id="38f06-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)


