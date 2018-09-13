---
title: Troubleshoot Azure Log Analytics Linux Agent | Microsoft Docs
description: Describe the symptoms, causes, and resolution for the most common issues with the Log Analytics Linux agent.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/14/2018
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 49a53b68fd394772f38b6040b80ec80c93d9c46c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869506"
---
# <a name="how-to-troubleshoot-issues-with-the-linux-agent-for-log-analytics"></a>How to troubleshoot issues with the Linux agent for Log Analytics

This article provides help troubleshooting errors you might experience with the Linux agent for Log Analytics and suggests possible solutions to resolve them.

## <a name="issue-unable-to-connect-through-proxy-to-log-analytics"></a>Issue: Unable to connect through proxy to Log Analytics

### <a name="probable-causes"></a>Probable causes
* The proxy specified during onboarding was incorrect
* The Log Analytics and Azure Automation Service Endpoints are not whitelisted in your datacenter 

### <a name="resolutions"></a>Resolutions
1. Reonboard to the Log Analytics service with the OMS Agent for Linux by using the following command with the option `-v` enabled. This allows verbose output of the agent connecting through the proxy to the OMS Service. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Review the section [Update proxy settings](log-analytics-agent-manage.md#update-proxy-settings) to verify you have properly configured the agent to communicate through a proxy server.    
* Double check that the following Log Analytics service endpoints are whitelisted:

    |Agent Resource| Ports | Direction |
    |------|---------|----------|  
    |*.ods.opinsights.azure.com | Port 443| Inbound and outbound |  
    |*.oms.opinsights.azure.com | Port 443| Inbound and outbound |  
    |*.blob.core.windows.net | Port 443| Inbound and outbound |  
    |*.azure-automation.net | Port 443| Inbound and outbound | 

## <a name="issue-you-receive-a-403-error-when-trying-to-onboard"></a>Issue: You receive a 403 error when trying to onboard

### <a name="probable-causes"></a>Probable causes
* Date and Time is incorrect on Linux Server 
* Workspace ID and Workspace Key used are not correct

### <a name="resolution"></a>Resolution

1. Check the time on your Linux server with the command date. If the time is +/- 15 minutes from current time, then onboarding fails. To correct this update the date and/or timezone of your Linux server. 
2. Verify you have installed the latest version of the OMS Agent for Linux.  The newest version now notifies you if time skew is causing the onboarding failure.
3. Reonboard using correct Workspace ID and Workspace Key following the installation instructions earlier in this topic.

## <a name="issue-you-see-a-500-and-404-error-in-the-log-file-right-after-onboarding"></a>Issue: You see a 500 and 404 error in the log file right after onboarding
This is a known issue that occurs on first upload of Linux data into a Log Analytics workspace. This does not affect data being sent or service experience.

## <a name="issue-you-are-not-seeing-any-data-in-the-azure-portal"></a>Issue: You are not seeing any data in the Azure portal

### <a name="probable-causes"></a>Probable causes

- Onboarding to the Log Analytics service failed
- Connection to the Log Analytics service is blocked
- OMS Agent for Linux data is backed up

### <a name="resolutions"></a>Resolutions
1. Check if onboarding the Log Analytics service was successful by checking if the following file exists: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. Reonboard using the `omsadmin.sh` command-line instructions
3. If using a proxy, refer to the proxy resolution steps provided earlier.
4. In some cases, when the OMS Agent for Linux cannot communicate with the service, data on the agent is queued to the full buffer size, which is 50 MB. The OMS Agent for Linux should be restarted by running the following command: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >This issue is fixed in agent version 1.1.0-28 and later.

