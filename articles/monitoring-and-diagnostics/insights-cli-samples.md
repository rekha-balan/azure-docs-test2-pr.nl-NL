---
title: Azure Monitor CLI quick start samples. | Microsoft Docs
description: Sample CLI commands for Azure Monitor features. Azure Monitor is a Microsoft Azure service which allows you to send alert notifications, call web URLs based on values of configured telemetry data, and autoScale Cloud Services, Virtual Machines, and Web Apps.
author: kamathashwin
manager: carolz
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: ashwink
ms.openlocfilehash: 0e629dac553f576f2dd3059453b00d6b10e48fd7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549075"
---
# <a name="azure-monitor--cross-platform-cli-quick-start-samples"></a><span data-ttu-id="cdd87-105">Azure Monitor  Cross-platform CLI quick start samples</span><span class="sxs-lookup"><span data-stu-id="cdd87-105">Azure Monitor  Cross-platform CLI quick start samples</span></span>
<span data-ttu-id="cdd87-106">This article shows you sample command-line interface (CLI) commands to help you access Azure Monitor features.</span><span class="sxs-lookup"><span data-stu-id="cdd87-106">This article shows you sample command-line interface (CLI) commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="cdd87-107">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span><span class="sxs-lookup"><span data-stu-id="cdd87-107">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="cdd87-108">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span><span class="sxs-lookup"><span data-stu-id="cdd87-108">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="cdd87-109">However, the namespaces and thus the commands below still contain the "insights".</span><span class="sxs-lookup"><span data-stu-id="cdd87-109">However, the namespaces and thus the commands below still contain the "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="cdd87-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cdd87-110">Prerequisites</span></span>
<span data-ttu-id="cdd87-111">If you haven't already installed the Azure CLI, see [Install the Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cdd87-111">If you haven't already installed the Azure CLI, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="cdd87-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cdd87-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="cdd87-113">In Windows, install npm from the [Node.js website](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="cdd87-113">In Windows, install npm from the [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="cdd87-114">After you complete the installation, using CMD.exe with Run As Administrator privileges, execute the following from the folder where npm is installed:</span><span class="sxs-lookup"><span data-stu-id="cdd87-114">After you complete the installation, using CMD.exe with Run As Administrator privileges, execute the following from the folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="cdd87-115">Next, navigate to any folder/location you want and type at the command-line:</span><span class="sxs-lookup"><span data-stu-id="cdd87-115">Next, navigate to any folder/location you want and type at the command-line:</span></span>

```console
azure help
```

## <a name="log-in-to-azure"></a><span data-ttu-id="cdd87-116">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="cdd87-116">Log in to Azure</span></span>
<span data-ttu-id="cdd87-117">The first step is to login to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="cdd87-117">The first step is to login to your Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="cdd87-118">After running this command, you have to sign in via the instructions on the screen.</span><span class="sxs-lookup"><span data-stu-id="cdd87-118">After running this command, you have to sign in via the instructions on the screen.</span></span> <span data-ttu-id="cdd87-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in the context of your default subscription.</span><span class="sxs-lookup"><span data-stu-id="cdd87-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in the context of your default subscription.</span></span>

<span data-ttu-id="cdd87-120">To list the details of your current subscription, use the following command.</span><span class="sxs-lookup"><span data-stu-id="cdd87-120">To list the details of your current subscription, use the following command.</span></span>

```console
azure account show
```

<span data-ttu-id="cdd87-121">To change working context to a different subscription, use the following command.</span><span class="sxs-lookup"><span data-stu-id="cdd87-121">To change working context to a different subscription, use the following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="cdd87-122">To use Azure Resource Manager and Azure Monitor commands, you need to be in Azure Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="cdd87-122">To use Azure Resource Manager and Azure Monitor commands, you need to be in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="cdd87-123">To view a list of all supported Azure Monitor commands, perform the following.</span><span class="sxs-lookup"><span data-stu-id="cdd87-123">To view a list of all supported Azure Monitor commands, perform the following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="cdd87-124">View activity log for a subscription</span><span class="sxs-lookup"><span data-stu-id="cdd87-124">View activity log for a subscription</span></span>
<span data-ttu-id="cdd87-125">To view a list of activity log events, perform the following.</span><span class="sxs-lookup"><span data-stu-id="cdd87-125">To view a list of activity log events, perform the following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="cdd87-126">Try the following to view all available options.</span><span class="sxs-lookup"><span data-stu-id="cdd87-126">Try the following to view all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="cdd87-127">Here is an example to list logs by a resourceGroup</span><span class="sxs-lookup"><span data-stu-id="cdd87-127">Here is an example to list logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="cdd87-128">Example to list logs by caller</span><span class="sxs-lookup"><span data-stu-id="cdd87-128">Example to list logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="cdd87-129">Example to list logs by caller on a resource type, within a start and end date</span><span class="sxs-lookup"><span data-stu-id="cdd87-129">Example to list logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="cdd87-130">Work with alerts</span><span class="sxs-lookup"><span data-stu-id="cdd87-130">Work with alerts</span></span>
<span data-ttu-id="cdd87-131">You can use the information in the section to work with alerts.</span><span class="sxs-lookup"><span data-stu-id="cdd87-131">You can use the information in the section to work with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="cdd87-132">Get alert rules in a resource group</span><span class="sxs-lookup"><span data-stu-id="cdd87-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="cdd87-133">Create a metric alert rule</span><span class="sxs-lookup"><span data-stu-id="cdd87-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-a-log-alert-rule"></a><span data-ttu-id="cdd87-134">Create a log alert rule</span><span class="sxs-lookup"><span data-stu-id="cdd87-134">Create a log alert rule</span></span>
```console
azure insights alerts rule log set ruleName eastus resourceGroupName someOperationName
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="cdd87-135">Create webtest alert rule</span><span class="sxs-lookup"><span data-stu-id="cdd87-135">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="cdd87-136">Delete an alert rule</span><span class="sxs-lookup"><span data-stu-id="cdd87-136">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="cdd87-137">Log profiles</span><span class="sxs-lookup"><span data-stu-id="cdd87-137">Log profiles</span></span>
<span data-ttu-id="cdd87-138">Use the information in this section to work with log profiles.</span><span class="sxs-lookup"><span data-stu-id="cdd87-138">Use the information in this section to work with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="cdd87-139">Get a log profile</span><span class="sxs-lookup"><span data-stu-id="cdd87-139">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="cdd87-140">Add a log profile without retention</span><span class="sxs-lookup"><span data-stu-id="cdd87-140">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="cdd87-141">Remove a log profile</span><span class="sxs-lookup"><span data-stu-id="cdd87-141">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="cdd87-142">Add a log profile with retention</span><span class="sxs-lookup"><span data-stu-id="cdd87-142">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="cdd87-143">Add a log profile with retention and EventHub</span><span class="sxs-lookup"><span data-stu-id="cdd87-143">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="cdd87-144">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="cdd87-144">Diagnostics</span></span>
<span data-ttu-id="cdd87-145">Use the information in this section to work with diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="cdd87-145">Use the information in this section to work with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="cdd87-146">Get a diagnostic setting</span><span class="sxs-lookup"><span data-stu-id="cdd87-146">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="cdd87-147">Disable a diagnostic setting</span><span class="sxs-lookup"><span data-stu-id="cdd87-147">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="cdd87-148">Enable a diagnostic setting without retention</span><span class="sxs-lookup"><span data-stu-id="cdd87-148">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="cdd87-149">Autoscale</span><span class="sxs-lookup"><span data-stu-id="cdd87-149">Autoscale</span></span>
<span data-ttu-id="cdd87-150">Use the information in this section to work with autoscale settings.</span><span class="sxs-lookup"><span data-stu-id="cdd87-150">Use the information in this section to work with autoscale settings.</span></span> <span data-ttu-id="cdd87-151">You need to modify these examples.</span><span class="sxs-lookup"><span data-stu-id="cdd87-151">You need to modify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="cdd87-152">Get autoscale settings for a resource group</span><span class="sxs-lookup"><span data-stu-id="cdd87-152">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="cdd87-153">Get autoscale settings by name in a resource group</span><span class="sxs-lookup"><span data-stu-id="cdd87-153">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="cdd87-154">Set auotoscale settings</span><span class="sxs-lookup"><span data-stu-id="cdd87-154">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
