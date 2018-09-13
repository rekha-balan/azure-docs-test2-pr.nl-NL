---
title: Service Map in Operations Management Suite (OMS) | Microsoft Docs
description: Service Map is an Operations Management Suite (OMS) solution that automatically discovers application components on Windows and Linux systems and maps the communication between services.  This article provides details for deploying Service Map in your environment and using it in a variety of scenarios.
services: operations-management-suite
documentationcenter: ''
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 66376c8665e7bd548af89972c10d131d4d8a7bf1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662938"
---
# <a name="using-service-map-solution-in-operations-management-suite-oms"></a>Using Service Map solution in Operations Management Suite (OMS)
Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services. It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.  Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.

This article describes the details of using Service Map.  For information on configuring Service Map and onboarding agents, see [Configuring Service Map solution in Operations Management Suite (OMS)](operations-management-suite-service-map-configure.md)


## <a name="use-cases-make-your-it-processes-dependency-aware"></a>Use cases: Make your IT processes dependency aware

### <a name="discovery"></a>Discovery
Service Map automatically builds a common reference map of dependencies across your servers, processes, and third-party services.  It discovers and maps all TCP dependencies, identifying surprise connections, remote third-party systems you depend on, and dependencies to traditional dark areas of your network such as Active Directory.  Service Map discovers failed network connections that your managed systems are attempting to make, helping you identify potential server misconfiguration, service outages, and network issues.

### <a name="incident-management"></a>Incident management
Service Map helps eliminate the guesswork of problem isolation by showing you how systems are connected and affecting each other.  In addition to failed connections, information about connected clients helps identify misconfigured load balancers, surprising or excessive load on critical services, and rogue clients such as developer machines talking to production systems.  Integrated workflows with OMS Change Tracking also allow you to see whether a change event on a back-end machine or service explains the root cause of an incident.

### <a name="migration-assurance"></a>Migration assurance
Service Map allows you to effectively plan, accelerate, and validate Azure migrations, ensuring that nothing is left behind and there are no surprise outages.  You can discover all interdependent systems that need to migrate together, assess system configuration and capacity, and identify whether a running system is still serving users or is a candidate for decommissioning instead of migration.  After the move is done, you can check on client load and identity to verify that test systems and customers are connecting.  If your subnet planning and firewall definitions have issues, failed connections in Service Map maps will point you to the systems that need connectivity.

### <a name="business-continuity"></a>Business continuity
If you are using Azure Site Recovery and need help defining the recovery sequence for your application environment, Service Map can automatically show you how systems rely on each other to ensure that your recovery plan is reliable.  By choosing a critical server and viewing its clients, you can identify the front-end systems that should be recovered only after that critical server is restored and available.  Conversely, by looking at a critical server’s back-end dependencies, you can identify those systems that must be recovered before your focus system is restored.

### <a name="patch-management"></a>Patch management
Service Map enhances your use of OMS System Update Assessment by showing you which other teams and servers depend on your service, so you can notify them in advance before you take your systems down for patching.  Service Map also enhances patch management in OMS by showing you whether your services are available and properly connected after they are patched and restarted.


## <a name="mapping-overview"></a>Mapping overview
Service Map agents gather information about all TCP-connected processes on the server where they’re installed, as well as details about the inbound and outbound connections for each process.  Using the Machine List on the left side of the Service Map solution, machines with Service Map agents can be selected to visualize their dependencies over a selected time range.  Machine dependency maps focus on a specific machine, and show all the machines that are direct TCP clients or servers of that machine.

![Service Map overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/service-map-overview.png)

Machines can be expanded in the map to show the running processes with active network connections during the selected time range.  When a remote machine with a Service Map agent is expanded to show process details, only those processes communicating with the focus machine are shown.  The count of agentless front-end machines connecting into the focus machine is indicated on the left side of the processes they connect to.  If the focus machine is making a connection to a back-end machine without an agent, that back-end server is included in a Server Port Group, along with other connections to the same port number.

By default, Service Map maps show the last 10 minutes of dependency information.  Using the time controls in the upper left, maps can be queried for historical time ranges, up to one-hour wide, to show how dependencies looked in the past, e.g. during an incident or before a change occurred.    Service Map data is stored for 30 days in paid workspaces, and for 7 days in free workspaces.

## <a name="status-badges-and-border-coloring"></a>Status badges and border coloring
At the bottom of each server in the map can be a list of status badges conveying status information about the server.  The badges indicate that there is some relevant information for the server from one of the OMS solution integrations.  Clicking on a badge will take you directly to the details of the status in in the right panel.  The currently availably status badges include Alerts, Changes, Security, and Updates.

Based on the severity of the status badges, machine node borders can be colored red (Critical), yellow (Warning), or blue (Informational).  The color represents the most severe status of any of the status badges.  A grey border indicates a node with no current status indicators.

![Status badges](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/status-badges.png)

## <a name="role-icons"></a>Role icons
Certain processes serve particular roles on machines: web servers, application servers, database, etc.  Service Map will annotate process and machine boxes with role icons to help identify at a glance the role a process or server plays.

| Role Icon | Description |
|:--|:--|
| ![Web server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/role-web-server.png) | Web Server |
| ![App server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/role-application-server.png) | Application Server |
| ![Database server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/role-database.png) | Database Server |
| ![LDAP server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/role-ldap.png) | LDAP Server |
| ![SMB server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/role-smb.png) | SMB Server |

![Role icons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a>Failed connections
Failed Connections are shown in Service Map maps for processes and computers, with a dashed red line showing if a client system is failing to reach a process or port.  Failed connections are reported from any system with a deployed Service Map agent if that system is the one attempting the failed connection.  Service Map measures this by observing TCP sockets that fail to establish a connection.  This could be due to a firewall, a misconfiguration in the client or server, or a remote service being unavailable.

![Failed connections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/failed-connections.png)

Understanding failed connections can help with troubleshooting, migration validation, security analysis, and overall architectural understanding.  Sometimes failed connections are harmless, but they often point directly to a problem, such as a failover environment suddenly becoming unreachable, …or two application tiers not being able to talk after a cloud migration.

## <a name="client-groups"></a>Client Groups
Client Groups are boxes on the map that represent client machines that do not have Dependency Agents.  A single Client Group represents the clients for an individual process.

![Client groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/client-groups.png)

To see the IP addresses of the servers in a Client Group, select the group.  The contents of the group will be listed in the Properties Panel.

![Client group properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a>Server Port Groups
Server Port Groups are boxes that represent server ports on servers that do not have Dependency Agents.  The box will list the server port along with a count of the number of servers with connections to that port.  Expand the box to see the individual servers and connections.  If there is only one server in the box, the name or IP address will be listed.

![Server port groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a>Context menu
Clicking on the three dots in the top right of any server will expose the context menu for that server.

![Failed connections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a>Load Server Map
Load Server Map will navigate to a new map with the selected server as the new Focus Machine.

### <a name="showhide-self-links"></a>Show/Hide Self Links
Show Self Links will redraw the server node including any self links, which are TCP connections that start and end on processes within the server.  If self links are shown, the menu will change to Hide Self Links, allowing users to toggle the drawing of self links.

## <a name="computer-summary"></a>Computer summary
The Machine Summary panel includes an overview of a server's Operating System and dependency counts along with a variety of data from other OMS solutions, including Performance Metrics, Change Tracking, Security, Updates, etc.

![Machine summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a>Computer and process properties
When navigating a Service Map map, you can select machines and processes to gain additional context about their properties.  Machines provide information about DNS name, IPv4 addresses, CPU and Memory capacity, VM Type, Operating System version, Last Reboot time, and the IDs of their OMS and Service Map agents.

![Machine properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/machine-properties.png)

Process details are gathered from Operating System metadata about running processes, including process name, process description, user name and domain (on Windows), company name, product name, product version, working directory, command line, and process start time.

![Process properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/process-properties.png)

The Process Summary panel provides additional information about that process’s connectivity, including its bound ports, inbound and outbound connections, and failed connections.

![Process summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/process-summary.png)

## <a name="oms-alerts-integration"></a>OMS Alerts integration
Service Map integrates with OMS Alerts to show fired alerts for the selected server in the selected time range.  The server will show an icon if there are current alerts and the Machine Alerts Panel will list the alerts

![Machine Alerts Panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/machine-alerts.png)

Note that for Service Map to be able to display relevant alerts, the alert rule must be created so that it fires for a specific computer.  To create proper alerts:
- Include a clause to group by computer: "by Computer interval 1minute"
- Choose to alert based on Metric measurement

![Alert configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/alert-configuration.png)


## <a name="oms-log-events-integration"></a>OMS Log Events integration
Service Map integrates with Log Search to show a count of all available log events for the selected server during the selected time range.  You can click on any row in the list of event counts to jump to Log Search and see the individual log events.

![Log events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/log-events.png)

## <a name="oms-change-tracking-integration"></a>OMS Change Tracking integration
Service Map's integration with Change Tracking is automatic when both solutions are enabled and configured in your OMS workspace.

The Machine Change Tracking Panel shows a list of all changes, with the most recent first, along with a link to drill into Log Search for additional details.
![Machine Change Tracking Panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/change-tracking.png)

Following is a drill-down view of Configuration Change event after selecting **Show in Log Analytics**.
![Configuration Change Event](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/configuration-change-event.png)


## <a name="oms-performance-integration"></a>OMS Performance integration
The Machine Performance Panel shows standard performance metrics for the selected server.  The metrics include CPU Utilization, Memory Utilization, Network Bytes Sent and Received, and a list of the top processes by Network Bytes sent and received.  Note that to get the network performance data, you must also have enabled the Wire Data 2.0 solution in OMS.
![Machine Change Tracking Panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/machine-performance.png)


## <a name="oms-security-integration"></a>OMS Security integration
Service Map's integration with Security and Audit is automatic when both solutions are enabled and configured in your OMS workspace.

The Machine Security Panel shows data from the OMS Security and Audit solution for the selected server.  The panel will list a summary of any outstanding security issues for the server during the selected time range.  Clicking on any of the security issues will drill down into a Log Search for details about the security issues.
![Machine Change Tracking Panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/machine-security.png)


## <a name="oms-updates-integration"></a>OMS Updates integration
Service Map's integration with Update Management is automatic when both solutions are enabled and configured in your OMS workspace.

The Machine Updates Panel shows data from the OMS Update Management solution for the selected server.  The panel will list a summary of any missing updates for the server during the selected time range.
![Machine Change Tracking Panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a>Log Analytics records
Service Map's computer and process inventory data is available for [search](../log-analytics/log-analytics-log-searches.md) in Log Analytics.  This can be applied to scenarios including migration planning, capacity analysis, discovery, and ad hoc performance troubleshooting.

One record is generated per hour for each unique computer and process in addition to records generated when a process or computer starts or is on-boarded to Service Map.  These records have the properties in the following tables.  The fields and values in the ServiceMapComputer_CL events map to fields of the Machine resource in the ServiceMap ARM API.  The fields and values in the ServiceMapProcess_CL events map to the fields of the Process resource in the ServiceMap ARM API.  The ResourceName_s field matches the name field in the corresponding ARM resource. Note - as Service Map features grow, these fields are subject to change.


There are internally generated properties you can use to identify unique processes and computers:

- Computer - Use ResourceId or ResourceName_s to uniquely identify a computer within an OMS Workspace.
- Process - Use ResourceId to uniquely identify a process within an OMS Workspace. ResourceName_s is unique within the context of the machine on which the process is running (MachineResourceName_s) 

Since multiple records can exist for a given process and computer in a given time range, queries can return more than one record for the same computer or process. To include only the most recent record add "| dedup ResourceId" to the query.

### <a name="servicemapcomputercl-records"></a>ServiceMapComputer_CL records
Records with a type of **ServiceMapComputer_CL** have inventory data for servers with Service Map agents.  These records have the properties in the following table:

| Property | Description |
|:--|:--|
| Type | *ServiceMapComputer_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | unique identifier for machine within the workspace |
| ResourceName_s | unique identifier for machine within workspace |
| ComputerName_s | computer FQDN |
| Ipv4Addresses_s | a list of the server's IPv4 addresses |
| Ipv6Addresses_s | a list of the server's IPv6 addresses |
| DnsNames_s | array of DNS names |
| OperatingSystemFamily_s | windows or linux |
| OperatingSystemFullName_s | operating system full name  |
| Bitness_s | bitness of machine (32bit) or (64bit) |
| PhysicalMemory_d | physical memory in MB |
| Cpus_d | number of cpus |
| CpuSpeed_d | cpu speed in MHz|
| VirtualizationState_s | "unknown", "physical", "virtual", "hypervisor" |
| VirtualMachineType_s | "hyperv", "vmware", etc. |
| VirtualMachineNativeMachineId_g | VM ID as assigned by its hypervisor |
| VirtualMachineName_s | VM name |
| BootTime_t | boot time |



### <a name="servicemapprocesscl-type-records"></a>ServiceMapProcess_CL Type records
Records with a type of **ServiceMapProcess_CL** have inventory data for TCP-connected processes on servers with Service Map agents.  These records have the properties in the following table:

| Property | Description |
|:--|:--|
| Type | *ServiceMapProcess_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | unique identifier for process within the workspace |
| ResourceName_s | unique identifier for process within machine on which it is running|
| MachineResourceName_s | machine resource name |
| ExecutableName_s | process executable name |
| StartTime_t | process pool start time |
| FirstPid_d | first pid in process pool |
| Description_s | process description |
| CompanyName_s | company name |
| InternalName_s | internal name |
| ProductName_s | product name |
| ProductVersion_s | product version |
| FileVersion_s | file version |
| CommandLine_s | command line |
| ExecutablePath _s | path to executable file |
| WorkingDirectory_s | working directory |
| UserName | account under which the process is executing |
| UserDomain | domain under which the process is executing |


## <a name="sample-log-searches"></a>Sample log searches

### <a name="list-all-known-machines"></a>List all known machines
Type=ServiceMapComputer_CL | dedup ResourceId

### <a name="list-the-physical-memory-capacity-of-all-managed-computers"></a>List the physical memory capacity of all managed computers.
Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId

### <a name="list-computer-name-dns-ip-and-os"></a>List computer name, DNS, IP, and OS.
Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId

### <a name="find-all-processes-with-sql-in-the-command-line"></a>Find all processes with "sql" in the command line
Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-resource-name"></a>Find a machine (most recent record) by resource name
Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-ip-address"></a>Find a machine (most recent record) by ip address
Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId

### <a name="list-all-known-processes-on-a-given-machine"></a>List all known processes on a given machine
Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="list-all-computers-running-sql"></a>List all computers running SQL
Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s

### <a name="list-of-all-unique-product-versions-of-curl-in-my-datacenter"></a>List of all unique product versions of curl in my datacenter
Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s

### <a name="create-a-computer-group-of-all-computers-running-centos"></a>Create a Computer Group of all computers running CentOS
Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s


## <a name="rest-api"></a>REST API
All of the server, process, and dependency data in Service Map is available via the [Service Map REST API](https://docs.microsoft.com/rest/api/servicemap/).


## <a name="diagnostic-and-usage-data"></a>Diagnostic and usage data
Microsoft automatically collects usage and performance data through your use of the Service Map service. Microsoft uses this Data to provide and improve the quality, security, and integrity of the Service Map service. Data includes information about the configuration of your software like operating system and version and also includes IP address, DNS name, and Workstation name in order to provide accurate and efficient troubleshooting capabilities. We do not collect names, addresses, or other contact information.

For more information on data collection and usage, please see the [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132).


## <a name="next-steps"></a>Next steps
- Learn more about [log searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to retrieve data collected by Service Map.


## <a name="troubleshooting"></a>Troubleshooting
- See the [Troubleshooting section of the Configuring Service Map document](operations-management-suite-service-map-configure.md#troubleshooting).


## <a name="feedback"></a>Feedback
Do you have any feedback for us about Service Map or this documentation?  Please visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote up existing suggestions.

























