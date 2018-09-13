---
title: Azure Monitor partner integrations | Microsoft Docs
description: Learn about Azure Monitor's partners and how you can access documentation for integrating with them.
author: johnkemnetz
manager: rboucher
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 01ee13ac-66fc-4edc-8b0c-32f69b986a26
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/10/2017
ms.author: johnkem
ms.openlocfilehash: 0ee43fe699b741cfe42a3bff902d2e5775825c32
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564276"
---
# <a name="azure-monitor-partner-integrations"></a><span data-ttu-id="57a86-103">Azure Monitor partner integrations</span><span class="sxs-lookup"><span data-stu-id="57a86-103">Azure Monitor partner integrations</span></span>
| <span data-ttu-id="57a86-104">Partners</span><span class="sxs-lookup"><span data-stu-id="57a86-104">Partners</span></span> |  |  |
| --- | --- | --- |
| <span data-ttu-id="57a86-105">[![Partner Logo][alertlogic-logo]<br/>**AlertLogic**][alertlogic-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-105">[![Partner Logo][alertlogic-logo]<br/>**AlertLogic**][alertlogic-anchor]</span></span> | <span data-ttu-id="57a86-106">[![Partner Logo][appdynamics-logo]<br/>**AppDynamics**][appdynamics-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-106">[![Partner Logo][appdynamics-logo]<br/>**AppDynamics**][appdynamics-anchor]</span></span> | <span data-ttu-id="57a86-107">[![Partner Logo][atlassian-logo]<br/>**Atlassian**][atlassian-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-107">[![Partner Logo][atlassian-logo]<br/>**Atlassian**][atlassian-anchor]</span></span> |
| <span data-ttu-id="57a86-108">[![Partner Logo][cloudhealth-logo]<br/>**CloudHealth**][cloudhealth-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-108">[![Partner Logo][cloudhealth-logo]<br/>**CloudHealth**][cloudhealth-anchor]</span></span> | <span data-ttu-id="57a86-109">[![Partner Logo][cloudmonix-logo]<br/>**CloudMonix**][cloudmonix-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-109">[![Partner Logo][cloudmonix-logo]<br/>**CloudMonix**][cloudmonix-anchor]</span></span> | <span data-ttu-id="57a86-110">[![Partner Logo][cloudyn-logo]<br/>**Cloudyn**][cloudyn-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-110">[![Partner Logo][cloudyn-logo]<br/>**Cloudyn**][cloudyn-anchor]</span></span> |
| <span data-ttu-id="57a86-111">[![Partner Logo][datadog-logo]<br/>**DataDog**][datadog-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-111">[![Partner Logo][datadog-logo]<br/>**DataDog**][datadog-anchor]</span></span> | <span data-ttu-id="57a86-112">[![Partner Logo][dynatrace-logo]<br/>**Dynatrace**][dynatrace-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-112">[![Partner Logo][dynatrace-logo]<br/>**Dynatrace**][dynatrace-anchor]</span></span> | <span data-ttu-id="57a86-113">[![Partner Logo][newrelic-logo]<br/>**NewRelic**][newrelic-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-113">[![Partner Logo][newrelic-logo]<br/>**NewRelic**][newrelic-anchor]</span></span> |
| <span data-ttu-id="57a86-114">[![Partner Logo][opsgenie-logo]<br/>**OpsGenie**][opsgenie-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-114">[![Partner Logo][opsgenie-logo]<br/>**OpsGenie**][opsgenie-anchor]</span></span> | <span data-ttu-id="57a86-115">[![Partner Logo][pagerduty-logo]<br/>**PagerDuty**][pagerduty-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-115">[![Partner Logo][pagerduty-logo]<br/>**PagerDuty**][pagerduty-anchor]</span></span> | <span data-ttu-id="57a86-116">[![Partner Logo][sciencelogic-logo]<br/>**ScienceLogic**][sciencelogic-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-116">[![Partner Logo][sciencelogic-logo]<br/>**ScienceLogic**][sciencelogic-anchor]</span></span> |
| <span data-ttu-id="57a86-117">[![Partner Logo][splunk-logo]<br/>**Splunk**][splunk-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-117">[![Partner Logo][splunk-logo]<br/>**Splunk**][splunk-anchor]</span></span> | <span data-ttu-id="57a86-118">[![Partner Logo][sumologic-logo]<br/>**Sumo Logic**][sumologic-anchor]</span><span class="sxs-lookup"><span data-stu-id="57a86-118">[![Partner Logo][sumologic-logo]<br/>**Sumo Logic**][sumologic-anchor]</span></span> | |

## <a name="alertlogic-log-manager"></a><span data-ttu-id="57a86-119">AlertLogic Log Manager</span><span class="sxs-lookup"><span data-stu-id="57a86-119">AlertLogic Log Manager</span></span>
<span data-ttu-id="57a86-120">Alert Logic Log Manager collects VM, Application, and Azure platform logs for security analysis and retention.</span><span class="sxs-lookup"><span data-stu-id="57a86-120">Alert Logic Log Manager collects VM, Application, and Azure platform logs for security analysis and retention.</span></span> <span data-ttu-id="57a86-121">This includes Azure Audit Logs via the Azure Monitor API.</span><span class="sxs-lookup"><span data-stu-id="57a86-121">This includes Azure Audit Logs via the Azure Monitor API.</span></span>  <span data-ttu-id="57a86-122">This information is used to detect malfeasance and meet compliance requirements.</span><span class="sxs-lookup"><span data-stu-id="57a86-122">This information is used to detect malfeasance and meet compliance requirements.</span></span>

<span data-ttu-id="57a86-123">[Go to the documentation.][alertlogic-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-123">[Go to the documentation.][alertlogic-doc]</span></span>

## <a name="appdynamics"></a><span data-ttu-id="57a86-124">AppDynamics</span><span class="sxs-lookup"><span data-stu-id="57a86-124">AppDynamics</span></span>
<span data-ttu-id="57a86-125">AppDynamics Application Performance Management (APM) enables application owners to rapidly troubleshoot performance bottlenecks and optimize the performance of their applications running in Azure environment.</span><span class="sxs-lookup"><span data-stu-id="57a86-125">AppDynamics Application Performance Management (APM) enables application owners to rapidly troubleshoot performance bottlenecks and optimize the performance of their applications running in Azure environment.</span></span> <span data-ttu-id="57a86-126">AppDynamics APM is seamlessly integrated with Azure Marketplace and available for monitor Azure Cloud Services (PaaS) (Including web & worker roles), Virtual Machines (IaaS), Remote Service Detection (Microsoft Azure Service Bus), Microsoft Azure Queue Microsoft Azure Remote Services (Azure Blob), Azure Queue (Microsoft Service Bus), Data Storage, Microsoft Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="57a86-126">AppDynamics APM is seamlessly integrated with Azure Marketplace and available for monitor Azure Cloud Services (PaaS) (Including web & worker roles), Virtual Machines (IaaS), Remote Service Detection (Microsoft Azure Service Bus), Microsoft Azure Queue Microsoft Azure Remote Services (Azure Blob), Azure Queue (Microsoft Service Bus), Data Storage, Microsoft Azure Blob Storage.</span></span>

<span data-ttu-id="57a86-127">[Go to the documentation.][appdynamics-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-127">[Go to the documentation.][appdynamics-doc]</span></span>

## <a name="atlassian-jira"></a><span data-ttu-id="57a86-128">Atlassian JIRA</span><span class="sxs-lookup"><span data-stu-id="57a86-128">Atlassian JIRA</span></span>
<span data-ttu-id="57a86-129">You can create JIRA tickets on Azure Monitor alerts.</span><span class="sxs-lookup"><span data-stu-id="57a86-129">You can create JIRA tickets on Azure Monitor alerts.</span></span>

<span data-ttu-id="57a86-130">[Go to the documentation.][atlassian-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-130">[Go to the documentation.][atlassian-doc]</span></span>

## <a name="cloudhealth"></a><span data-ttu-id="57a86-131">CloudHealth</span><span class="sxs-lookup"><span data-stu-id="57a86-131">CloudHealth</span></span>
<span data-ttu-id="57a86-132">Unite and automate your cloud with a platform built to save serious time and money.</span><span class="sxs-lookup"><span data-stu-id="57a86-132">Unite and automate your cloud with a platform built to save serious time and money.</span></span> <span data-ttu-id="57a86-133">With unparalleled visibility, intuitive optimization and rock-solid governance practices, CloudHealth is redefining cloud management.</span><span class="sxs-lookup"><span data-stu-id="57a86-133">With unparalleled visibility, intuitive optimization and rock-solid governance practices, CloudHealth is redefining cloud management.</span></span> <span data-ttu-id="57a86-134">The Cloudhealth platform enables enterprises and MSPs to maximize return on cloud investments and make confident decisions around cost, usage, performance and security.</span><span class="sxs-lookup"><span data-stu-id="57a86-134">The Cloudhealth platform enables enterprises and MSPs to maximize return on cloud investments and make confident decisions around cost, usage, performance and security.</span></span>

<span data-ttu-id="57a86-135">[Learn More.][cloudhealth-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-135">[Learn More.][cloudhealth-doc]</span></span>

## <a name="cloudmonix"></a><span data-ttu-id="57a86-136">CloudMonix</span><span class="sxs-lookup"><span data-stu-id="57a86-136">CloudMonix</span></span>
<span data-ttu-id="57a86-137">CloudMonix offers monitoring, automation and self-healing services for Microsoft Azure platform.</span><span class="sxs-lookup"><span data-stu-id="57a86-137">CloudMonix offers monitoring, automation and self-healing services for Microsoft Azure platform.</span></span>

<span data-ttu-id="57a86-138">[Go to the documentation.][cloudmonix-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-138">[Go to the documentation.][cloudmonix-doc]</span></span>

## <a name="cloudyn"></a><span data-ttu-id="57a86-139">Cloudyn</span><span class="sxs-lookup"><span data-stu-id="57a86-139">Cloudyn</span></span>
<span data-ttu-id="57a86-140">Cloudyn manages and optimizes multi-platform, hybrid cloud deployments to help enterprises fully realize their cloud potential.</span><span class="sxs-lookup"><span data-stu-id="57a86-140">Cloudyn manages and optimizes multi-platform, hybrid cloud deployments to help enterprises fully realize their cloud potential.</span></span> <span data-ttu-id="57a86-141">The SaaS solution delivers visibility into usage, performance and cost, coupled with insights and actionable recommendations for smart optimization and cloud governance.</span><span class="sxs-lookup"><span data-stu-id="57a86-141">The SaaS solution delivers visibility into usage, performance and cost, coupled with insights and actionable recommendations for smart optimization and cloud governance.</span></span> <span data-ttu-id="57a86-142">Cloudyn enables accountability through accurate chargeback and hierarchical cost allocation management.</span><span class="sxs-lookup"><span data-stu-id="57a86-142">Cloudyn enables accountability through accurate chargeback and hierarchical cost allocation management.</span></span> <span data-ttu-id="57a86-143">Cloudyn is integrated with Azure Monitoring in order to provide insights and actionable recommendations in order to optimize your Azure deployment.</span><span class="sxs-lookup"><span data-stu-id="57a86-143">Cloudyn is integrated with Azure Monitoring in order to provide insights and actionable recommendations in order to optimize your Azure deployment.</span></span>

<span data-ttu-id="57a86-144">[Go to the documentation.][cloudyn-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-144">[Go to the documentation.][cloudyn-doc]</span></span>

## <a name="datadog"></a><span data-ttu-id="57a86-145">DataDog</span><span class="sxs-lookup"><span data-stu-id="57a86-145">DataDog</span></span>
<span data-ttu-id="57a86-146">Datadog is the world’s leading monitoring service for cloud-scale applications, bringing together data from servers, databases, tools and services to present a unified view of your entire stack.</span><span class="sxs-lookup"><span data-stu-id="57a86-146">Datadog is the world’s leading monitoring service for cloud-scale applications, bringing together data from servers, databases, tools and services to present a unified view of your entire stack.</span></span> <span data-ttu-id="57a86-147">These capabilities are provided on a SaaS-based data analytics platform that enables Dev and Ops teams to work collaboratively to avoid downtime, resolve performance problems, and ensure that development and deployment cycles finish on time.</span><span class="sxs-lookup"><span data-stu-id="57a86-147">These capabilities are provided on a SaaS-based data analytics platform that enables Dev and Ops teams to work collaboratively to avoid downtime, resolve performance problems, and ensure that development and deployment cycles finish on time.</span></span> <span data-ttu-id="57a86-148">By integrating Datadog and Azure, you can collect and view metrics from across your infrastructure, correlate VM metrics with application-level metrics, and slice and dice your metrics using any combination of properties and custom tags.</span><span class="sxs-lookup"><span data-stu-id="57a86-148">By integrating Datadog and Azure, you can collect and view metrics from across your infrastructure, correlate VM metrics with application-level metrics, and slice and dice your metrics using any combination of properties and custom tags.</span></span>

<span data-ttu-id="57a86-149">[Go to the documentation.][datadog-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-149">[Go to the documentation.][datadog-doc]</span></span>

## <a name="dynatrace"></a><span data-ttu-id="57a86-150">Dynatrace</span><span class="sxs-lookup"><span data-stu-id="57a86-150">Dynatrace</span></span>
<span data-ttu-id="57a86-151">The Dynatrace OneAgent integrates with Azure VMs and App Services via the according Azure extension mechanisms.</span><span class="sxs-lookup"><span data-stu-id="57a86-151">The Dynatrace OneAgent integrates with Azure VMs and App Services via the according Azure extension mechanisms.</span></span>
<span data-ttu-id="57a86-152">This way we can gather performance metrics about hosts, network and services.</span><span class="sxs-lookup"><span data-stu-id="57a86-152">This way we can gather performance metrics about hosts, network and services.</span></span>
<span data-ttu-id="57a86-153">Besides just displaying metrics we visualize environments end-to-end, showing transactions from the client side to the database layer.</span><span class="sxs-lookup"><span data-stu-id="57a86-153">Besides just displaying metrics we visualize environments end-to-end, showing transactions from the client side to the database layer.</span></span>
<span data-ttu-id="57a86-154">AI-based correlation of problems and fully integrated root-cause-analysis, including method level insights into code and database, make troubleshooting and performance optimizations much easier.</span><span class="sxs-lookup"><span data-stu-id="57a86-154">AI-based correlation of problems and fully integrated root-cause-analysis, including method level insights into code and database, make troubleshooting and performance optimizations much easier.</span></span>

<span data-ttu-id="57a86-155">[Go to the documentation.][dynatrace-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-155">[Go to the documentation.][dynatrace-doc]</span></span>

## <a name="newrelic"></a><span data-ttu-id="57a86-156">NewRelic</span><span class="sxs-lookup"><span data-stu-id="57a86-156">NewRelic</span></span>
<span data-ttu-id="57a86-157">[Learn more.][newrelic-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-157">[Learn more.][newrelic-doc]</span></span>

## <a name="opsgenie"></a><span data-ttu-id="57a86-158">OpsGenie</span><span class="sxs-lookup"><span data-stu-id="57a86-158">OpsGenie</span></span>
<span data-ttu-id="57a86-159">OpsGenie acts as a dispatcher for the alerts generated by Azure.</span><span class="sxs-lookup"><span data-stu-id="57a86-159">OpsGenie acts as a dispatcher for the alerts generated by Azure.</span></span> <span data-ttu-id="57a86-160">OpsGenie determines the right people to notify based on on-call schedules and escalations, by notifying them using email, text messages (SMS), phone calls, push notifications.</span><span class="sxs-lookup"><span data-stu-id="57a86-160">OpsGenie determines the right people to notify based on on-call schedules and escalations, by notifying them using email, text messages (SMS), phone calls, push notifications.</span></span> <span data-ttu-id="57a86-161">Simply, Azure generates alerts for detected problems, and OpsGenie ensures the right people are working on them.</span><span class="sxs-lookup"><span data-stu-id="57a86-161">Simply, Azure generates alerts for detected problems, and OpsGenie ensures the right people are working on them.</span></span>

<span data-ttu-id="57a86-162">[Go to the documentation.][opsgenie-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-162">[Go to the documentation.][opsgenie-doc]</span></span>

## <a name="pagerduty"></a><span data-ttu-id="57a86-163">PagerDuty</span><span class="sxs-lookup"><span data-stu-id="57a86-163">PagerDuty</span></span>
<span data-ttu-id="57a86-164">PagerDuty, the leading incident management solution, has provided first-class support for Azure Alerts on metrics.</span><span class="sxs-lookup"><span data-stu-id="57a86-164">PagerDuty, the leading incident management solution, has provided first-class support for Azure Alerts on metrics.</span></span> <span data-ttu-id="57a86-165">Today, PagerDuty now supports notifications on Azure Monitor Alerts, Autoscale Notifications, and Audit Log Events, in addition to notifications on platform-level metrics for Azure services.</span><span class="sxs-lookup"><span data-stu-id="57a86-165">Today, PagerDuty now supports notifications on Azure Monitor Alerts, Autoscale Notifications, and Audit Log Events, in addition to notifications on platform-level metrics for Azure services.</span></span> <span data-ttu-id="57a86-166">These enhancements give users increased visibility into the core Azure Platform while enabling them to take full advantage of PagerDuty’s incident management capabilities for real-time response.</span><span class="sxs-lookup"><span data-stu-id="57a86-166">These enhancements give users increased visibility into the core Azure Platform while enabling them to take full advantage of PagerDuty’s incident management capabilities for real-time response.</span></span> <span data-ttu-id="57a86-167">Our expanded Azure integration is made possible via webhooks, allowing for quick and easy set-up and customization.</span><span class="sxs-lookup"><span data-stu-id="57a86-167">Our expanded Azure integration is made possible via webhooks, allowing for quick and easy set-up and customization.</span></span>

<span data-ttu-id="57a86-168">[Go to the documentation.][pagerduty-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-168">[Go to the documentation.][pagerduty-doc]</span></span>

## <a name="sciencelogic"></a><span data-ttu-id="57a86-169">ScienceLogic</span><span class="sxs-lookup"><span data-stu-id="57a86-169">ScienceLogic</span></span>
<span data-ttu-id="57a86-170">ScienceLogic delivers the next generation IT service assurance platform for managing any technology, anywhere.</span><span class="sxs-lookup"><span data-stu-id="57a86-170">ScienceLogic delivers the next generation IT service assurance platform for managing any technology, anywhere.</span></span>  <span data-ttu-id="57a86-171">In one platform, ScienceLogic delivers the scale, security, automation, and resiliency necessary to simplify the ever-expanding task of managing IT resources, services, and applications that are in constant motion.</span><span class="sxs-lookup"><span data-stu-id="57a86-171">In one platform, ScienceLogic delivers the scale, security, automation, and resiliency necessary to simplify the ever-expanding task of managing IT resources, services, and applications that are in constant motion.</span></span>  <span data-ttu-id="57a86-172">The ScienceLogic platform uses Azure APIs to interface with Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="57a86-172">The ScienceLogic platform uses Azure APIs to interface with Microsoft Azure.</span></span>  <span data-ttu-id="57a86-173">ScienceLogic gives you real-time visibility into your Azure services and resources so you know when something’s not working and can fix it faster.</span><span class="sxs-lookup"><span data-stu-id="57a86-173">ScienceLogic gives you real-time visibility into your Azure services and resources so you know when something’s not working and can fix it faster.</span></span> <span data-ttu-id="57a86-174">You can also manage Azure alongside your other clouds and data center systems and services.</span><span class="sxs-lookup"><span data-stu-id="57a86-174">You can also manage Azure alongside your other clouds and data center systems and services.</span></span>

<span data-ttu-id="57a86-175">[Learn more.][sciencelogic-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-175">[Learn more.][sciencelogic-doc]</span></span>

## <a name="splunk-add-on-for-microsoft-cloud-services"></a><span data-ttu-id="57a86-176">Splunk Add-on for Microsoft Cloud Services</span><span class="sxs-lookup"><span data-stu-id="57a86-176">Splunk Add-on for Microsoft Cloud Services</span></span>
<span data-ttu-id="57a86-177">The Splunk Add-on for Microsoft Cloud Services is [available in the Splunkbase here](https://splunkbase.splunk.com/app/3110/).</span><span class="sxs-lookup"><span data-stu-id="57a86-177">The Splunk Add-on for Microsoft Cloud Services is [available in the Splunkbase here](https://splunkbase.splunk.com/app/3110/).</span></span>

<span data-ttu-id="57a86-178">[Go to the documentation.][splunk-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-178">[Go to the documentation.][splunk-doc]</span></span>

## <a name="sumo-logic"></a><span data-ttu-id="57a86-179">Sumo Logic</span><span class="sxs-lookup"><span data-stu-id="57a86-179">Sumo Logic</span></span>
<span data-ttu-id="57a86-180">Sumo Logic is a secure, cloud-native, machine data analytics service, delivering real-time, continuous intelligence from structured, semi-structured and unstructured data across the entire application lifecycle and stack.</span><span class="sxs-lookup"><span data-stu-id="57a86-180">Sumo Logic is a secure, cloud-native, machine data analytics service, delivering real-time, continuous intelligence from structured, semi-structured and unstructured data across the entire application lifecycle and stack.</span></span> <span data-ttu-id="57a86-181">More than 1,000 customers around the globe rely on Sumo Logic for the analytics and insights to build, run and secure their modern applications and cloud infrastructures.</span><span class="sxs-lookup"><span data-stu-id="57a86-181">More than 1,000 customers around the globe rely on Sumo Logic for the analytics and insights to build, run and secure their modern applications and cloud infrastructures.</span></span> <span data-ttu-id="57a86-182">With Sumo Logic, customers gain a multi-tenant, service-model advantage to accelerate their shift to continuous innovation, increasing competitive advantage, business value and growth.</span><span class="sxs-lookup"><span data-stu-id="57a86-182">With Sumo Logic, customers gain a multi-tenant, service-model advantage to accelerate their shift to continuous innovation, increasing competitive advantage, business value and growth.</span></span>

<span data-ttu-id="57a86-183">[Learn more.][sumologic-doc]</span><span class="sxs-lookup"><span data-stu-id="57a86-183">[Learn more.][sumologic-doc]</span></span>

## <a name="next-steps"></a><span data-ttu-id="57a86-184">Next Steps</span><span class="sxs-lookup"><span data-stu-id="57a86-184">Next Steps</span></span>
* [<span data-ttu-id="57a86-185">Learn more about Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="57a86-185">Learn more about Azure Monitor</span></span>](monitoring-overview.md)
* [<span data-ttu-id="57a86-186">Access metrics using the REST API</span><span class="sxs-lookup"><span data-stu-id="57a86-186">Access metrics using the REST API</span></span>](monitoring-rest-api-walkthrough.md)
* [<span data-ttu-id="57a86-187">Stream the Activity Log to a 3rd party service</span><span class="sxs-lookup"><span data-stu-id="57a86-187">Stream the Activity Log to a 3rd party service</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="57a86-188">Stream Diagnostic Logs to a 3rd party service</span><span class="sxs-lookup"><span data-stu-id="57a86-188">Stream Diagnostic Logs to a 3rd party service</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

<!--Partner Anchors-->
[alertlogic-anchor]: #alertlogic-log-manager "AlertLogic"
[appdynamics-anchor]: #appdynamics "AppDynamics"
[atlassian-anchor]: #atlassian-jira "Atlassian"
[cloudhealth-anchor]: #cloudhealth "CloudHealth"
[cloudmonix-anchor]: #cloudmonix "CloudMonix"
[cloudyn-anchor]: #cloudyn "Cloudyn"
[datadog-anchor]: #datadog "DataDog"
[dynatrace-anchor]: #dynatrace "Dynatrace"
[newrelic-anchor]: #newrelic "NewRelic"
[opsgenie-anchor]: #opsgenie "OpsGenie"
[pagerduty-anchor]: #pagerduty "PagerDuty"
[sciencelogic-anchor]: #sciencelogic "ScienceLogic"
[splunk-anchor]: #splunk-add-on-for-microsoft-cloud-services "Splunk"
[sumologic-anchor]: #sumo-logic "Sumo Logic"

<!--Icon references-->
[alertlogic-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/alertlogic.png
[appdynamics-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/appdynamics.png
[atlassian-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/atlassian.png
[cloudhealth-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/cloudhealth.png
[cloudmonix-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/cloudmonix.png
[cloudyn-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/cloudyn.png
[datadog-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/datadog.png
[dynatrace-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/dynatrace.png
[newrelic-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/newrelic.png
[opsgenie-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/opsgenie.png
[pagerduty-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/pagerduty.png
[sciencelogic-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/sciencelogic.png
[splunk-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/splunk.png
[sumologic-logo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/partner-logos/sumologic.png

<!--Partner Documentation-->
[alertlogic-doc]: https://docs.alertlogic.com/userGuides/log-manager-collection-sources.htm "AlertLogic documentation."
[appdynamics-doc]: https://docs.appdynamics.com/display/PRO42/Register+for+AppDynamics+for+Windows+Azure "AppDynamics documentation."
[atlassian-doc]: https://azure.microsoft.com/blog/automated-notifications-from-azure-monitor-for-atlassian-jira/
[cloudhealth-doc]: https://www.cloudhealthtech.com/azure
[cloudmonix-doc]: http://cloudmonix.com/features/azure-management/ "CloudMonix introduction."
[cloudyn-doc]: https://www.cloudyn.com/azure-monitoring "Cloudyn introduction."
[datadog-doc]: http://docs.datadoghq.com/integrations/azure/ "DataDog documentation."
[dynatrace-doc]: https://blog.ruxit.com/ruxit-monitoring-azure-web-apps/ "Dynatrace documentation."
[newrelic-doc]: https://newrelic.com/azure "NewRelic documentation."
[opsgenie-doc]: https://www.opsgenie.com/docs/integrations/azure-integration "OpsGenie documentation."
[pagerduty-doc]: https://www.pagerduty.com/docs/guides/azure-integration-guide/ "PagerDuty documentation."
[sciencelogic-doc]: https://www.sciencelogic.com/product/technologies/microsoft/azure "ScienceLogic documentation."
[splunk-doc]: http://docs.splunk.com/Documentation/AddOns/released/MSCloudServices/About "Splunk documentation."
[sumologic-doc]: https://www.sumologic.com/azure "SumoLogic documentation."














