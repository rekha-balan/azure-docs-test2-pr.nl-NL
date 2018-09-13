---
title: Deploy Azure Log Analytics Nozzle for Cloud Foundry monitoring | Microsoft Docs
description: Step-by-step guidance on deploying the Cloud Foundry loggregator Nozzle for Azure Log Analytics. Use the Nozzle to monitor the Cloud Foundry system health and performance metrics.
services: virtual-machines-linux
documentationcenter: ''
author: ningk
manager: jeconnoc
editor: ''
tags: Cloud-Foundry
ms.assetid: 00c76c49-3738-494b-b70d-344d8efc0853
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: ningk
ms.openlocfilehash: c58c2b255d269aef7e8b3fea62d003ad0c16ef0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857181"
---
# <a name="deploy-azure-log-analytics-nozzle-for-cloud-foundry-system-monitoring"></a><span data-ttu-id="8c0e7-104">Deploy Azure Log Analytics Nozzle for Cloud Foundry system monitoring</span><span class="sxs-lookup"><span data-stu-id="8c0e7-104">Deploy Azure Log Analytics Nozzle for Cloud Foundry system monitoring</span></span>

<span data-ttu-id="8c0e7-105">[Azure Log Analytics](https://azure.microsoft.com/services/log-analytics/) is a service in Azure.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-105">[Azure Log Analytics](https://azure.microsoft.com/services/log-analytics/) is a service in Azure.</span></span> <span data-ttu-id="8c0e7-106">It helps you collect and analyze data that is generated from your cloud and on-premises environments.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-106">It helps you collect and analyze data that is generated from your cloud and on-premises environments.</span></span>

<span data-ttu-id="8c0e7-107">The Log Analytics Nozzle (the Nozzle) is a Cloud Foundry (CF) component, which forwards metrics from the [Cloud Foundry loggregator](https://docs.cloudfoundry.org/loggregator/architecture.html) firehose to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-107">The Log Analytics Nozzle (the Nozzle) is a Cloud Foundry (CF) component, which forwards metrics from the [Cloud Foundry loggregator](https://docs.cloudfoundry.org/loggregator/architecture.html) firehose to Log Analytics.</span></span> <span data-ttu-id="8c0e7-108">With the Nozzle, you can collect, view, and analyze your CF system health and performance metrics, across multiple deployments.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-108">With the Nozzle, you can collect, view, and analyze your CF system health and performance metrics, across multiple deployments.</span></span>

<span data-ttu-id="8c0e7-109">In this document, you learn how to deploy the Nozzle to your CF environment, and then access the data from the Log Analytics console.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-109">In this document, you learn how to deploy the Nozzle to your CF environment, and then access the data from the Log Analytics console.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c0e7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8c0e7-110">Prerequisites</span></span>

<span data-ttu-id="8c0e7-111">The following steps are prerequisites for deploying the Nozzle.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-111">The following steps are prerequisites for deploying the Nozzle.</span></span>

### <a name="1-deploy-a-cf-or-pivotal-cloud-foundry-environment-in-azure"></a><span data-ttu-id="8c0e7-112">1. Deploy a CF or Pivotal Cloud Foundry environment in Azure</span><span class="sxs-lookup"><span data-stu-id="8c0e7-112">1. Deploy a CF or Pivotal Cloud Foundry environment in Azure</span></span>

<span data-ttu-id="8c0e7-113">You can use the Nozzle with either an open source CF deployment or a Pivotal Cloud Foundry (PCF) deployment.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-113">You can use the Nozzle with either an open source CF deployment or a Pivotal Cloud Foundry (PCF) deployment.</span></span>

* [<span data-ttu-id="8c0e7-114">Deploy Cloud Foundry on Azure</span><span class="sxs-lookup"><span data-stu-id="8c0e7-114">Deploy Cloud Foundry on Azure</span></span>](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md)

* [<span data-ttu-id="8c0e7-115">Deploy Pivotal Cloud Foundry on Azure</span><span class="sxs-lookup"><span data-stu-id="8c0e7-115">Deploy Pivotal Cloud Foundry on Azure</span></span>](https://docs.pivotal.io/pivotalcf/1-11/customizing/azure.html)

### <a name="2-install-the-cf-command-line-tools-for-deploying-the-nozzle"></a><span data-ttu-id="8c0e7-116">2. Install the CF command-line tools for deploying the Nozzle</span><span class="sxs-lookup"><span data-stu-id="8c0e7-116">2. Install the CF command-line tools for deploying the Nozzle</span></span>

<span data-ttu-id="8c0e7-117">The Nozzle runs as an application in CF environment.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-117">The Nozzle runs as an application in CF environment.</span></span> <span data-ttu-id="8c0e7-118">You need CF CLI to deploy the application.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-118">You need CF CLI to deploy the application.</span></span>

<span data-ttu-id="8c0e7-119">The Nozzle also needs access permission to the loggregator firehose and the Cloud Controller.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-119">The Nozzle also needs access permission to the loggregator firehose and the Cloud Controller.</span></span> <span data-ttu-id="8c0e7-120">To create and configure the user, you need the User Account and Authentication (UAA) service.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-120">To create and configure the user, you need the User Account and Authentication (UAA) service.</span></span>

* [<span data-ttu-id="8c0e7-121">Install Cloud Foundry CLI</span><span class="sxs-lookup"><span data-stu-id="8c0e7-121">Install Cloud Foundry CLI</span></span>](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)

* [<span data-ttu-id="8c0e7-122">Install Cloud Foundry UAA command-line client</span><span class="sxs-lookup"><span data-stu-id="8c0e7-122">Install Cloud Foundry UAA command-line client</span></span>](https://github.com/cloudfoundry/cf-uaac/blob/master/README.md)

<span data-ttu-id="8c0e7-123">Before setting up the UAA command-Line client, ensure that Rubygems is installed.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-123">Before setting up the UAA command-Line client, ensure that Rubygems is installed.</span></span>

### <a name="3-create-a-log-analytics-workspace-in-azure"></a><span data-ttu-id="8c0e7-124">3. Create a Log Analytics workspace in Azure</span><span class="sxs-lookup"><span data-stu-id="8c0e7-124">3. Create a Log Analytics workspace in Azure</span></span>

<span data-ttu-id="8c0e7-125">You can create the Log Analytics workspace manually or by using a template.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-125">You can create the Log Analytics workspace manually or by using a template.</span></span> <span data-ttu-id="8c0e7-126">The template will deploy a setup of pre-configured OMS KPI views and alerts for the OMS console.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-126">The template will deploy a setup of pre-configured OMS KPI views and alerts for the OMS console.</span></span> 

#### <a name="to-create-the-workspace-manually"></a><span data-ttu-id="8c0e7-127">To create the workspace manually:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-127">To create the workspace manually:</span></span>

1. <span data-ttu-id="8c0e7-128">In the Azure portal, search the list of services in the Azure Marketplace, and then select Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-128">In the Azure portal, search the list of services in the Azure Marketplace, and then select Log Analytics.</span></span>
2. <span data-ttu-id="8c0e7-129">Select **Create**, and then select choices for the following items:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-129">Select **Create**, and then select choices for the following items:</span></span>

   * <span data-ttu-id="8c0e7-130">**OMS Workspace**: Type a name for your workspace.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-130">**OMS Workspace**: Type a name for your workspace.</span></span>
   * <span data-ttu-id="8c0e7-131">**Subscription**: If you have multiple subscriptions, choose the one that is the same as your CF deployment.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-131">**Subscription**: If you have multiple subscriptions, choose the one that is the same as your CF deployment.</span></span>
   * <span data-ttu-id="8c0e7-132">**Resource group**: You can create a new resource group, or use the same one with your CF deployment.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-132">**Resource group**: You can create a new resource group, or use the same one with your CF deployment.</span></span>
   * <span data-ttu-id="8c0e7-133">**Location**: Enter the location.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-133">**Location**: Enter the location.</span></span>
   * <span data-ttu-id="8c0e7-134">**Pricing tier**: Select **OK** to complete.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-134">**Pricing tier**: Select **OK** to complete.</span></span>

<span data-ttu-id="8c0e7-135">For more information, see [Get started with Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started).</span><span class="sxs-lookup"><span data-stu-id="8c0e7-135">For more information, see [Get started with Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started).</span></span>

#### <a name="to-create-the-oms-workspace-through-the-oms-monitoring-template-from-azure-market-place"></a><span data-ttu-id="8c0e7-136">To create the OMS workspace through the OMS monitoring template from Azure market place:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-136">To create the OMS workspace through the OMS monitoring template from Azure market place:</span></span>

1. <span data-ttu-id="8c0e7-137">Open Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-137">Open Azure portal.</span></span>
2. <span data-ttu-id="8c0e7-138">Click the "+" sign, or "Create a resource" on the top left corner.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-138">Click the "+" sign, or "Create a resource" on the top left corner.</span></span>
3. <span data-ttu-id="8c0e7-139">Type "Cloud Foundry" in the search window, select "OMS Cloud Foundry Monitoring Solution".</span><span class="sxs-lookup"><span data-stu-id="8c0e7-139">Type "Cloud Foundry" in the search window, select "OMS Cloud Foundry Monitoring Solution".</span></span>
4. <span data-ttu-id="8c0e7-140">The OMS Cloud Foundry monitoring solution template front page is loaded, click "Create" to launch the template blade.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-140">The OMS Cloud Foundry monitoring solution template front page is loaded, click "Create" to launch the template blade.</span></span>
5. <span data-ttu-id="8c0e7-141">Enter the required parameters:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-141">Enter the required parameters:</span></span>
    * <span data-ttu-id="8c0e7-142">**Subscription**: Select an Azure subscription for the OMS workspace, usually the same with Cloud Foundry deployment.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-142">**Subscription**: Select an Azure subscription for the OMS workspace, usually the same with Cloud Foundry deployment.</span></span>
    * <span data-ttu-id="8c0e7-143">**Resource group**: Select an existing resource group or create a new one for the OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-143">**Resource group**: Select an existing resource group or create a new one for the OMS workspace.</span></span>
    * <span data-ttu-id="8c0e7-144">**Resource Group Location**: Select the location of the resource group.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-144">**Resource Group Location**: Select the location of the resource group.</span></span>
    * <span data-ttu-id="8c0e7-145">**OMS_Workspace_Name**: Enter a workspace name, if the workspace does not exist, the template will create a new one.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-145">**OMS_Workspace_Name**: Enter a workspace name, if the workspace does not exist, the template will create a new one.</span></span>
    * <span data-ttu-id="8c0e7-146">**OMS_Workspace_Region**: Select the location for the workspace.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-146">**OMS_Workspace_Region**: Select the location for the workspace.</span></span>
    * <span data-ttu-id="8c0e7-147">**OMS_Workspace_Pricing_Tier**: Select the OMS workspace SKU.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-147">**OMS_Workspace_Pricing_Tier**: Select the OMS workspace SKU.</span></span> <span data-ttu-id="8c0e7-148">See the [pricing guidance](https://azure.microsoft.com/pricing/details/log-analytics/) for reference.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-148">See the [pricing guidance](https://azure.microsoft.com/pricing/details/log-analytics/) for reference.</span></span>
    * <span data-ttu-id="8c0e7-149">**Legal terms**: Click Legal terms, then click “Create” to accept the legal term.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-149">**Legal terms**: Click Legal terms, then click “Create” to accept the legal term.</span></span>
- <span data-ttu-id="8c0e7-150">After all parameters are specified, click “Create” to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-150">After all parameters are specified, click “Create” to deploy the template.</span></span> <span data-ttu-id="8c0e7-151">When the deployment is completed, the status will show up at the notification tab.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-151">When the deployment is completed, the status will show up at the notification tab.</span></span>


## <a name="deploy-the-nozzle"></a><span data-ttu-id="8c0e7-152">Deploy the Nozzle</span><span class="sxs-lookup"><span data-stu-id="8c0e7-152">Deploy the Nozzle</span></span>

<span data-ttu-id="8c0e7-153">There are a couple of different ways to deploy the Nozzle: as a PCF tile or as a CF application.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-153">There are a couple of different ways to deploy the Nozzle: as a PCF tile or as a CF application.</span></span>

### <a name="deploy-the-nozzle-as-a-pcf-ops-manager-tile"></a><span data-ttu-id="8c0e7-154">Deploy the Nozzle as a PCF Ops Manager tile</span><span class="sxs-lookup"><span data-stu-id="8c0e7-154">Deploy the Nozzle as a PCF Ops Manager tile</span></span>

<span data-ttu-id="8c0e7-155">Follow the steps to [install and configure the Azure Log Analytics Nozzle for PCF](http://docs.pivotal.io/partners/azure-log-analytics-nozzle/installing.html).This is the simplified approach, the PCF Ops manager tile will automatically configure and push the nozzle.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-155">Follow the steps to [install and configure the Azure Log Analytics Nozzle for PCF](http://docs.pivotal.io/partners/azure-log-analytics-nozzle/installing.html).This is the simplified approach, the PCF Ops manager tile will automatically configure and push the nozzle.</span></span> 

### <a name="deploy-the-nozzle-manually-as-a-cf-application"></a><span data-ttu-id="8c0e7-156">Deploy the Nozzle manually as a CF application</span><span class="sxs-lookup"><span data-stu-id="8c0e7-156">Deploy the Nozzle manually as a CF application</span></span>

<span data-ttu-id="8c0e7-157">If you are not using PCF Ops Manager, deploy the Nozzle as an application.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-157">If you are not using PCF Ops Manager, deploy the Nozzle as an application.</span></span> <span data-ttu-id="8c0e7-158">The following sections describe this process.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-158">The following sections describe this process.</span></span>

#### <a name="sign-in-to-your-cf-deployment-as-an-admin-through-cf-cli"></a><span data-ttu-id="8c0e7-159">Sign in to your CF deployment as an admin through CF CLI</span><span class="sxs-lookup"><span data-stu-id="8c0e7-159">Sign in to your CF deployment as an admin through CF CLI</span></span>

<span data-ttu-id="8c0e7-160">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-160">Run the following command:</span></span>
```
cf login -a https://api.${SYSTEM_DOMAIN} -u ${CF_USER} --skip-ssl-validation
```

<span data-ttu-id="8c0e7-161">"SYSTEM_DOMAIN" is your CF domain name.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-161">"SYSTEM_DOMAIN" is your CF domain name.</span></span> <span data-ttu-id="8c0e7-162">You can retrieve it by searching the "SYSTEM_DOMAIN" in your CF deployment manifest file.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-162">You can retrieve it by searching the "SYSTEM_DOMAIN" in your CF deployment manifest file.</span></span> 

<span data-ttu-id="8c0e7-163">"CF_User" is the CF admin name.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-163">"CF_User" is the CF admin name.</span></span> <span data-ttu-id="8c0e7-164">You can retrieve the name and password by searching the "scim" section, looking for the name and the "cf_admin_password" in your CF deployment manifest file.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-164">You can retrieve the name and password by searching the "scim" section, looking for the name and the "cf_admin_password" in your CF deployment manifest file.</span></span>

#### <a name="create-a-cf-user-and-grant-required-privileges"></a><span data-ttu-id="8c0e7-165">Create a CF user and grant required privileges</span><span class="sxs-lookup"><span data-stu-id="8c0e7-165">Create a CF user and grant required privileges</span></span>

<span data-ttu-id="8c0e7-166">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-166">Run the following commands:</span></span>
```
uaac target https://uaa.${SYSTEM_DOMAIN} --skip-ssl-validation
uaac token client get admin
cf create-user ${FIREHOSE_USER} ${FIREHOSE_USER_PASSWORD}
uaac member add cloud_controller.admin ${FIREHOSE_USER}
uaac member add doppler.firehose ${FIREHOSE_USER}
```

<span data-ttu-id="8c0e7-167">"SYSTEM_DOMAIN" is your CF domain name.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-167">"SYSTEM_DOMAIN" is your CF domain name.</span></span> <span data-ttu-id="8c0e7-168">You can retrieve it by searching the "SYSTEM_DOMAIN" in your CF deployment manifest file.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-168">You can retrieve it by searching the "SYSTEM_DOMAIN" in your CF deployment manifest file.</span></span>

#### <a name="download-the-latest-log-analytics-nozzle-release"></a><span data-ttu-id="8c0e7-169">Download the latest Log Analytics Nozzle release</span><span class="sxs-lookup"><span data-stu-id="8c0e7-169">Download the latest Log Analytics Nozzle release</span></span>

<span data-ttu-id="8c0e7-170">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-170">Run the following command:</span></span>
```
git clone https://github.com/Azure/oms-log-analytics-firehose-nozzle.git
cd oms-log-analytics-firehose-nozzle
```

#### <a name="set-environment-variables"></a><span data-ttu-id="8c0e7-171">Set environment variables</span><span class="sxs-lookup"><span data-stu-id="8c0e7-171">Set environment variables</span></span>

<span data-ttu-id="8c0e7-172">Now you can set environment variables in the manifest.yml file in your current directory.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-172">Now you can set environment variables in the manifest.yml file in your current directory.</span></span> <span data-ttu-id="8c0e7-173">The following shows the app manifest for the Nozzle.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-173">The following shows the app manifest for the Nozzle.</span></span> <span data-ttu-id="8c0e7-174">Replace values with your specific Log Analytics workspace information.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-174">Replace values with your specific Log Analytics workspace information.</span></span>

```
OMS_WORKSPACE             : Log Analytics workspace ID: open OMS portal from your Log Analytics workspace, select Settings, and select connected sources.
OMS_KEY                   : OMS key: open OMS portal from your Log Analytics workspace, select Settings, and select connected sources.
OMS_POST_TIMEOUT          : HTTP post timeout for sending events to Log Analytics. The default is 10 seconds.
OMS_BATCH_TIME            : Interval for posting a batch to Log Analytics. The default is 10 seconds.
OMS_MAX_MSG_NUM_PER_BATCH : The maximum number of messages in a batch to Log Analytics. The default is 1000.
API_ADDR                  : The API URL of the CF environment. For more information, see the preceding section, "Sign in to your CF deployment as an admin through CF CLI."
DOPPLER_ADDR              : Loggregator's traffic controller URL. For more information, see the preceding section, "Sign in to your CF deployment as an admin through CF CLI."
FIREHOSE_USER             : CF user you created in the preceding section, "Create a CF user and grant required privileges." This user has firehose and Cloud Controller admin access.
FIREHOSE_USER_PASSWORD    : Password of the CF user above.
EVENT_FILTER              : Event types to be filtered out. The format is a comma-separated list. Valid event types are METRIC, LOG, and HTTP.
SKIP_SSL_VALIDATION       : If true, allows insecure connections to the UAA and the traffic controller.
CF_ENVIRONMENT            : Enter any string value for identifying logs and metrics from different CF environments.
IDLE_TIMEOUT              : The Keep Alive duration for the firehose consumer. The default is 60 seconds.
LOG_LEVEL                 : The logging level of the Nozzle. Valid levels are DEBUG, INFO, and ERROR.
LOG_EVENT_COUNT           : If true, the total count of events that the Nozzle has received and sent are logged to Log Analytics as CounterEvents.
LOG_EVENT_COUNT_INTERVAL  : The time interval of the logging event count to Log Analytics. The default is 60 seconds.
```

### <a name="push-the-application-from-your-development-computer"></a><span data-ttu-id="8c0e7-175">Push the application from your development computer</span><span class="sxs-lookup"><span data-stu-id="8c0e7-175">Push the application from your development computer</span></span>

<span data-ttu-id="8c0e7-176">Ensure that you are under the oms-log-analytics-firehose-nozzle folder.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-176">Ensure that you are under the oms-log-analytics-firehose-nozzle folder.</span></span> <span data-ttu-id="8c0e7-177">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-177">Run the following command:</span></span>
```
cf push
```

## <a name="validate-the-nozzle-installation"></a><span data-ttu-id="8c0e7-178">Validate the Nozzle installation</span><span class="sxs-lookup"><span data-stu-id="8c0e7-178">Validate the Nozzle installation</span></span>

### <a name="from-apps-manager-for-pcf"></a><span data-ttu-id="8c0e7-179">From Apps Manager (for PCF)</span><span class="sxs-lookup"><span data-stu-id="8c0e7-179">From Apps Manager (for PCF)</span></span>

1. <span data-ttu-id="8c0e7-180">Sign in to Ops Manager, and make sure the tile is displayed on the installation dashboard.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-180">Sign in to Ops Manager, and make sure the tile is displayed on the installation dashboard.</span></span>
2. <span data-ttu-id="8c0e7-181">Sign in to Apps Manager, make sure the space you have created for the Nozzle is listed on the usage report, and confirm that the status is normal.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-181">Sign in to Apps Manager, make sure the space you have created for the Nozzle is listed on the usage report, and confirm that the status is normal.</span></span>

### <a name="from-your-development-computer"></a><span data-ttu-id="8c0e7-182">From your development computer</span><span class="sxs-lookup"><span data-stu-id="8c0e7-182">From your development computer</span></span>

<span data-ttu-id="8c0e7-183">In the CF CLI window, type:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-183">In the CF CLI window, type:</span></span>
```
cf apps
```
<span data-ttu-id="8c0e7-184">Make sure the OMS Nozzle application is running.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-184">Make sure the OMS Nozzle application is running.</span></span>

## <a name="view-the-data-in-the-oms-portal"></a><span data-ttu-id="8c0e7-185">View the data in the OMS portal</span><span class="sxs-lookup"><span data-stu-id="8c0e7-185">View the data in the OMS portal</span></span>

<span data-ttu-id="8c0e7-186">If you have deployed the OMS monitoring solution through the market place template, go to Azure portal and located the OMS solution.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-186">If you have deployed the OMS monitoring solution through the market place template, go to Azure portal and located the OMS solution.</span></span> <span data-ttu-id="8c0e7-187">You can find the solution in the resource group you specified in the template.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-187">You can find the solution in the resource group you specified in the template.</span></span> <span data-ttu-id="8c0e7-188">Click the solution, browse to the "OMS Console", the pre-configured views are listed, with top Cloud Foundry system KPIs, application data, alerts and VM health metrics.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-188">Click the solution, browse to the "OMS Console", the pre-configured views are listed, with top Cloud Foundry system KPIs, application data, alerts and VM health metrics.</span></span> 

<span data-ttu-id="8c0e7-189">If you have created the OMS workspace manually, follow steps below to create the views and alerts:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-189">If you have created the OMS workspace manually, follow steps below to create the views and alerts:</span></span>

### <a name="1-import-the-oms-view"></a><span data-ttu-id="8c0e7-190">1. Import the OMS view</span><span class="sxs-lookup"><span data-stu-id="8c0e7-190">1. Import the OMS view</span></span>

<span data-ttu-id="8c0e7-191">From the OMS portal, browse to **View Designer** > **Import** > **Browse**, and select one of the omsview files.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-191">From the OMS portal, browse to **View Designer** > **Import** > **Browse**, and select one of the omsview files.</span></span> <span data-ttu-id="8c0e7-192">For example, select *Cloud Foundry.omsview*, and save the view.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-192">For example, select *Cloud Foundry.omsview*, and save the view.</span></span> <span data-ttu-id="8c0e7-193">Now a tile is displayed on the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-193">Now a tile is displayed on the **Overview** page.</span></span> <span data-ttu-id="8c0e7-194">Select it to see visualized metrics.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-194">Select it to see visualized metrics.</span></span>

<span data-ttu-id="8c0e7-195">You can customize these views or create new views through **View Designer**.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-195">You can customize these views or create new views through **View Designer**.</span></span>

<span data-ttu-id="8c0e7-196">The *"Cloud Foundry.omsview"* is a preview version of the Cloud Foundry OMS view template.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-196">The *"Cloud Foundry.omsview"* is a preview version of the Cloud Foundry OMS view template.</span></span> <span data-ttu-id="8c0e7-197">This is a fully configured, default template.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-197">This is a fully configured, default template.</span></span> <span data-ttu-id="8c0e7-198">If you have suggestions or feedback about the template, send them to the [issue section](https://github.com/Azure/oms-log-analytics-firehose-nozzle/issues).</span><span class="sxs-lookup"><span data-stu-id="8c0e7-198">If you have suggestions or feedback about the template, send them to the [issue section](https://github.com/Azure/oms-log-analytics-firehose-nozzle/issues).</span></span>

### <a name="2-create-alert-rules"></a><span data-ttu-id="8c0e7-199">2. Create alert rules</span><span class="sxs-lookup"><span data-stu-id="8c0e7-199">2. Create alert rules</span></span>

<span data-ttu-id="8c0e7-200">You can [create the alerts](https://docs.microsoft.com/azure/log-analytics/log-analytics-alerts), and customize the queries and threshold values as needed.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-200">You can [create the alerts](https://docs.microsoft.com/azure/log-analytics/log-analytics-alerts), and customize the queries and threshold values as needed.</span></span> <span data-ttu-id="8c0e7-201">The following are recommended alerts:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-201">The following are recommended alerts:</span></span>

| <span data-ttu-id="8c0e7-202">Search query</span><span class="sxs-lookup"><span data-stu-id="8c0e7-202">Search query</span></span>                                                                  | <span data-ttu-id="8c0e7-203">Generate alert based on</span><span class="sxs-lookup"><span data-stu-id="8c0e7-203">Generate alert based on</span></span> | <span data-ttu-id="8c0e7-204">Description</span><span class="sxs-lookup"><span data-stu-id="8c0e7-204">Description</span></span>                                                                       |
| ----------------------------------------------------------------------------- | ----------------------- | --------------------------------------------------------------------------------- |
| <span data-ttu-id="8c0e7-205">Type=CF_ValueMetric_CL Origin_s=bbs Name_s="Domain.cf-apps"</span><span class="sxs-lookup"><span data-stu-id="8c0e7-205">Type=CF_ValueMetric_CL Origin_s=bbs Name_s="Domain.cf-apps"</span></span>                   | <span data-ttu-id="8c0e7-206">Number of results < 1</span><span class="sxs-lookup"><span data-stu-id="8c0e7-206">Number of results < 1</span></span>   | <span data-ttu-id="8c0e7-207">**bbs.Domain.cf-apps** indicates if the cf-apps Domain is up-to-date.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-207">**bbs.Domain.cf-apps** indicates if the cf-apps Domain is up-to-date.</span></span> <span data-ttu-id="8c0e7-208">This means that CF App requests from Cloud Controller are synchronized to bbs.LRPsDesired (Diego-desired AIs) for execution.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-208">This means that CF App requests from Cloud Controller are synchronized to bbs.LRPsDesired (Diego-desired AIs) for execution.</span></span> <span data-ttu-id="8c0e7-209">No data received means cf-apps Domain is not up-to-date in the specified time window.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-209">No data received means cf-apps Domain is not up-to-date in the specified time window.</span></span> |
| <span data-ttu-id="8c0e7-210">Type=CF_ValueMetric_CL Origin_s=rep Name_s=UnhealthyCell Value_d>1</span><span class="sxs-lookup"><span data-stu-id="8c0e7-210">Type=CF_ValueMetric_CL Origin_s=rep Name_s=UnhealthyCell Value_d>1</span></span>            | <span data-ttu-id="8c0e7-211">Number of results > 0</span><span class="sxs-lookup"><span data-stu-id="8c0e7-211">Number of results > 0</span></span>   | <span data-ttu-id="8c0e7-212">For Diego cells, 0 means healthy, and 1 means unhealthy.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-212">For Diego cells, 0 means healthy, and 1 means unhealthy.</span></span> <span data-ttu-id="8c0e7-213">Set the alert if multiple unhealthy Diego cells are detected in the specified time window.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-213">Set the alert if multiple unhealthy Diego cells are detected in the specified time window.</span></span> |
| <span data-ttu-id="8c0e7-214">Type=CF_ValueMetric_CL Origin_s="bosh-hm-forwarder" Name_s="system.healthy" Value_d=0</span><span class="sxs-lookup"><span data-stu-id="8c0e7-214">Type=CF_ValueMetric_CL Origin_s="bosh-hm-forwarder" Name_s="system.healthy" Value_d=0</span></span> | <span data-ttu-id="8c0e7-215">Number of results > 0</span><span class="sxs-lookup"><span data-stu-id="8c0e7-215">Number of results > 0</span></span> | <span data-ttu-id="8c0e7-216">1 means the system is healthy, and 0 means the system is not healthy.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-216">1 means the system is healthy, and 0 means the system is not healthy.</span></span> |
| <span data-ttu-id="8c0e7-217">Type=CF_ValueMetric_CL Origin_s=route_emitter Name_s=ConsulDownMode Value_d>0</span><span class="sxs-lookup"><span data-stu-id="8c0e7-217">Type=CF_ValueMetric_CL Origin_s=route_emitter Name_s=ConsulDownMode Value_d>0</span></span> | <span data-ttu-id="8c0e7-218">Number of results > 0</span><span class="sxs-lookup"><span data-stu-id="8c0e7-218">Number of results > 0</span></span>   | <span data-ttu-id="8c0e7-219">Consul emits its health status periodically.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-219">Consul emits its health status periodically.</span></span> <span data-ttu-id="8c0e7-220">0 means the system is healthy, and 1 means that the route emitter detects that Consul is down.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-220">0 means the system is healthy, and 1 means that the route emitter detects that Consul is down.</span></span> |
| <span data-ttu-id="8c0e7-221">Type=CF_CounterEvent_CL Origin_s=DopplerServer (Name_s="TruncatingBuffer.DroppedMessages" or Name_s="doppler.shedEnvelopes") Delta_d>0</span><span class="sxs-lookup"><span data-stu-id="8c0e7-221">Type=CF_CounterEvent_CL Origin_s=DopplerServer (Name_s="TruncatingBuffer.DroppedMessages" or Name_s="doppler.shedEnvelopes") Delta_d>0</span></span> | <span data-ttu-id="8c0e7-222">Number of results > 0</span><span class="sxs-lookup"><span data-stu-id="8c0e7-222">Number of results > 0</span></span> | <span data-ttu-id="8c0e7-223">The delta number of messages intentionally dropped by Doppler due to back pressure.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-223">The delta number of messages intentionally dropped by Doppler due to back pressure.</span></span> |
| <span data-ttu-id="8c0e7-224">Type=CF_LogMessage_CL SourceType_s=LGR MessageType_s=ERR</span><span class="sxs-lookup"><span data-stu-id="8c0e7-224">Type=CF_LogMessage_CL SourceType_s=LGR MessageType_s=ERR</span></span>                      | <span data-ttu-id="8c0e7-225">Number of results > 0</span><span class="sxs-lookup"><span data-stu-id="8c0e7-225">Number of results > 0</span></span>   | <span data-ttu-id="8c0e7-226">Loggregator emits **LGR** to indicate problems with the logging process.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-226">Loggregator emits **LGR** to indicate problems with the logging process.</span></span> <span data-ttu-id="8c0e7-227">An example of such a problem is when the log message output is too high.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-227">An example of such a problem is when the log message output is too high.</span></span> |
| <span data-ttu-id="8c0e7-228">Type=CF_ValueMetric_CL Name_s=slowConsumerAlert</span><span class="sxs-lookup"><span data-stu-id="8c0e7-228">Type=CF_ValueMetric_CL Name_s=slowConsumerAlert</span></span>                               | <span data-ttu-id="8c0e7-229">Number of results > 0</span><span class="sxs-lookup"><span data-stu-id="8c0e7-229">Number of results > 0</span></span>   | <span data-ttu-id="8c0e7-230">When the Nozzle receives a slow consumer alert from loggregator, it sends the **slowConsumerAlert** ValueMetric to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-230">When the Nozzle receives a slow consumer alert from loggregator, it sends the **slowConsumerAlert** ValueMetric to Log Analytics.</span></span> |
| <span data-ttu-id="8c0e7-231">Type=CF_CounterEvent_CL Job_s=nozzle Name_s=eventsLost Delta_d>0</span><span class="sxs-lookup"><span data-stu-id="8c0e7-231">Type=CF_CounterEvent_CL Job_s=nozzle Name_s=eventsLost Delta_d>0</span></span>              | <span data-ttu-id="8c0e7-232">Number of results > 0</span><span class="sxs-lookup"><span data-stu-id="8c0e7-232">Number of results > 0</span></span>   | <span data-ttu-id="8c0e7-233">If the delta number of lost events reaches a threshold, it means the Nozzle might have a problem running.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-233">If the delta number of lost events reaches a threshold, it means the Nozzle might have a problem running.</span></span> |

## <a name="scale"></a><span data-ttu-id="8c0e7-234">Scale</span><span class="sxs-lookup"><span data-stu-id="8c0e7-234">Scale</span></span>

<span data-ttu-id="8c0e7-235">You can scale the Nozzle and the loggregator.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-235">You can scale the Nozzle and the loggregator.</span></span>

### <a name="scale-the-nozzle"></a><span data-ttu-id="8c0e7-236">Scale the Nozzle</span><span class="sxs-lookup"><span data-stu-id="8c0e7-236">Scale the Nozzle</span></span>

<span data-ttu-id="8c0e7-237">You should start with at least two instances of the Nozzle.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-237">You should start with at least two instances of the Nozzle.</span></span> <span data-ttu-id="8c0e7-238">The firehose distributes the workload across all instances of the Nozzle.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-238">The firehose distributes the workload across all instances of the Nozzle.</span></span>
<span data-ttu-id="8c0e7-239">To make sure the Nozzle can keep up with the data traffic from the firehose, set up the **slowConsumerAlert** alert (listed in the preceding section, "Create alert rules").</span><span class="sxs-lookup"><span data-stu-id="8c0e7-239">To make sure the Nozzle can keep up with the data traffic from the firehose, set up the **slowConsumerAlert** alert (listed in the preceding section, "Create alert rules").</span></span> <span data-ttu-id="8c0e7-240">After you have been alerted, follow the [guidance for slow Nozzle](https://docs.pivotal.io/pivotalcf/1-11/loggregator/log-ops-guide.html#slow-noz) to determine whether scaling is needed.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-240">After you have been alerted, follow the [guidance for slow Nozzle](https://docs.pivotal.io/pivotalcf/1-11/loggregator/log-ops-guide.html#slow-noz) to determine whether scaling is needed.</span></span>
<span data-ttu-id="8c0e7-241">To scale up the Nozzle, use Apps Manager or the CF CLI to increase the instance numbers or the memory or disk resources for the Nozzle.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-241">To scale up the Nozzle, use Apps Manager or the CF CLI to increase the instance numbers or the memory or disk resources for the Nozzle.</span></span>

### <a name="scale-the-loggregator"></a><span data-ttu-id="8c0e7-242">Scale the loggregator</span><span class="sxs-lookup"><span data-stu-id="8c0e7-242">Scale the loggregator</span></span>

<span data-ttu-id="8c0e7-243">Loggregator sends an **LGR** log message to indicate problems with the logging process.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-243">Loggregator sends an **LGR** log message to indicate problems with the logging process.</span></span> <span data-ttu-id="8c0e7-244">You can monitor the alert to determine whether the loggregator needs to be scaled up.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-244">You can monitor the alert to determine whether the loggregator needs to be scaled up.</span></span>
<span data-ttu-id="8c0e7-245">To scale up the loggregator, either increase the Doppler buffer size, or add additional Doppler server instances in the CF manifest.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-245">To scale up the loggregator, either increase the Doppler buffer size, or add additional Doppler server instances in the CF manifest.</span></span> <span data-ttu-id="8c0e7-246">For more information, see [the guidance for scaling the loggregator](https://docs.cloudfoundry.org/running/managing-cf/logging-config.html#scaling).</span><span class="sxs-lookup"><span data-stu-id="8c0e7-246">For more information, see [the guidance for scaling the loggregator](https://docs.cloudfoundry.org/running/managing-cf/logging-config.html#scaling).</span></span>

## <a name="update"></a><span data-ttu-id="8c0e7-247">Update</span><span class="sxs-lookup"><span data-stu-id="8c0e7-247">Update</span></span>

<span data-ttu-id="8c0e7-248">To update the Nozzle with a newer version, download the new Nozzle release, follow the steps in the preceding "Deploy the Nozzle" section, and push the application again.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-248">To update the Nozzle with a newer version, download the new Nozzle release, follow the steps in the preceding "Deploy the Nozzle" section, and push the application again.</span></span>

### <a name="remove-the-nozzle-from-ops-manager"></a><span data-ttu-id="8c0e7-249">Remove the Nozzle from Ops Manager</span><span class="sxs-lookup"><span data-stu-id="8c0e7-249">Remove the Nozzle from Ops Manager</span></span>

1. <span data-ttu-id="8c0e7-250">Sign in to Ops Manager.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-250">Sign in to Ops Manager.</span></span>
2. <span data-ttu-id="8c0e7-251">Locate the **Microsoft Azure Log Analytics Nozzle for PCF** tile.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-251">Locate the **Microsoft Azure Log Analytics Nozzle for PCF** tile.</span></span>
3. <span data-ttu-id="8c0e7-252">Select the garbage icon, and confirm the deletion.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-252">Select the garbage icon, and confirm the deletion.</span></span>

### <a name="remove-the-nozzle-from-your-development-computer"></a><span data-ttu-id="8c0e7-253">Remove the Nozzle from your development computer</span><span class="sxs-lookup"><span data-stu-id="8c0e7-253">Remove the Nozzle from your development computer</span></span>

<span data-ttu-id="8c0e7-254">In your CF CLI window, type:</span><span class="sxs-lookup"><span data-stu-id="8c0e7-254">In your CF CLI window, type:</span></span>
```
cf delete <App Name> -r
```

<span data-ttu-id="8c0e7-255">If you remove the Nozzle, the data in OMS portal is not automatically removed.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-255">If you remove the Nozzle, the data in OMS portal is not automatically removed.</span></span> <span data-ttu-id="8c0e7-256">It expires based on your Log Analytics retention setting.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-256">It expires based on your Log Analytics retention setting.</span></span>

## <a name="support-and-feedback"></a><span data-ttu-id="8c0e7-257">Support and feedback</span><span class="sxs-lookup"><span data-stu-id="8c0e7-257">Support and feedback</span></span>

<span data-ttu-id="8c0e7-258">Azure Log Analytics Nozzle is open sourced.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-258">Azure Log Analytics Nozzle is open sourced.</span></span> <span data-ttu-id="8c0e7-259">Send your questions and feedback to the [GitHub section](https://github.com/Azure/oms-log-analytics-firehose-nozzle/issues).</span><span class="sxs-lookup"><span data-stu-id="8c0e7-259">Send your questions and feedback to the [GitHub section](https://github.com/Azure/oms-log-analytics-firehose-nozzle/issues).</span></span> <span data-ttu-id="8c0e7-260">To open an Azure support request, choose "Virtual Machine running Cloud Foundry" as the service category.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-260">To open an Azure support request, choose "Virtual Machine running Cloud Foundry" as the service category.</span></span> 

## <a name="next-step"></a><span data-ttu-id="8c0e7-261">Next step</span><span class="sxs-lookup"><span data-stu-id="8c0e7-261">Next step</span></span>

<span data-ttu-id="8c0e7-262">From PCF2.0, VM performance metrics are transferred to Azure log analytics nozzle by System Metrics Forwarder, and integrated into the OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-262">From PCF2.0, VM performance metrics are transferred to Azure log analytics nozzle by System Metrics Forwarder, and integrated into the OMS workspace.</span></span> <span data-ttu-id="8c0e7-263">You no longer need the OMS agent for the VM performance metrics.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-263">You no longer need the OMS agent for the VM performance metrics.</span></span> <span data-ttu-id="8c0e7-264">However you can still use the OMS agent to collect Syslog information.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-264">However you can still use the OMS agent to collect Syslog information.</span></span> <span data-ttu-id="8c0e7-265">The OMS agent is installed as a Bosh add-on to your CF VMs.</span><span class="sxs-lookup"><span data-stu-id="8c0e7-265">The OMS agent is installed as a Bosh add-on to your CF VMs.</span></span> 

<span data-ttu-id="8c0e7-266">For details, see [Deploy OMS agent to your Cloud Foundry deployment](https://github.com/Azure/oms-agent-for-linux-boshrelease).</span><span class="sxs-lookup"><span data-stu-id="8c0e7-266">For details, see [Deploy OMS agent to your Cloud Foundry deployment](https://github.com/Azure/oms-agent-for-linux-boshrelease).</span></span>
