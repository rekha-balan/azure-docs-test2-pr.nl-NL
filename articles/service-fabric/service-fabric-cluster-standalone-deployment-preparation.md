---
title: Azure Service Fabric Standalone Cluster Deployment Preparation | Microsoft Docs
description: Documentation related to preparing the environment and creating the cluster configuration, to be considered prior to deploying a cluster intended for handling a production workload.
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: ''
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: f332193f9a53260173a1010b8bf9f08726bea427
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549565"
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Plan and prepare your Service Fabric standalone cluster deployment
Perform the following steps before you create your cluster.

### <a name="step-1-plan-your-cluster-infrastructure"></a>Step 1: Plan your cluster infrastructure
You are about to create a Service Fabric cluster on machines you own, so you can decide what kinds of failures you want the cluster to survive. For example, do you need separate power lines or Internet connections supplied to these machines? In addition, consider the physical security of these machines. Where are the machines located and who needs access to them? After you make these decisions, you can logically map the machines to the various fault domains (see Step 4). The infrastructure planning for production clusters is more involved than for test clusters.

### <a name="step-2-prepare-the-machines-to-meet-the-prerequisites"></a>Step 2: Prepare the machines to meet the prerequisites
Prerequisites for each machine that you want to add to the cluster:

* A minimum of 16 GB of RAM is recommended.
* A minimum of 40 of GB available disk space is recommended.
* A 4 core or greater CPU is recommended.
* Connectivity to a secure network or networks for all machines.
* Windows Server 2012 R2 or Windows Server 2016. 
* [.NET Framework 4.5.1 or higher](https://www.microsoft.com/download/details.aspx?id=40773), full install.
* [Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* The [RemoteRegistry service](https://technet.microsoft.com/library/cc754820) should be running on all the machines.

The cluster administrator deploying and configuring the cluster must have [administrator privileges](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) on each of the machines. You cannot install Service Fabric on a domain controller.

### <a name="step-3-determine-the-initial-cluster-size"></a>Step 3: Determine the initial cluster size
Each node in a standalone Service Fabric cluster has the Service Fabric runtime deployed and is a member of the cluster. In a typical production deployment, there is one node per OS instance (physical or virtual). The cluster size is determined by your business needs. However, you must have a minimum cluster size of three nodes (machines or virtual machines).
For development purposes, you can have more than one node on a given machine. In a production environment, Service Fabric supports only one node per physical or virtual machine.

### <a name="step-4-determine-the-number-of-fault-domains-and-upgrade-domains"></a>Step 4: Determine the number of fault domains and upgrade domains
A *fault domain* (FD) is a physical unit of failure and is directly related to the physical infrastructure in the data centers. A fault domain consists of hardware components (computers, switches, networks, and more) that share a single point of failure. Although there is no 1:1 mapping between fault domains and racks, loosely speaking, each rack can be considered a fault domain. When considering the nodes in your cluster, we strongly recommend that the nodes be distributed among at least three fault domains.

When you specify FDs in ClusterConfig.json, you can choose the name for each FD. Service Fabric supports hierarchical FDs, so you can reflect your infrastructure topology in them.  For example, the following FDs are valid:

* "faultDomain": "fd:/Room1/Rack1/Machine1"
* "faultDomain": "fd:/FD1"
* "faultDomain": "fd:/Room1/Rack1/PDU1/M1"

An *upgrade domain* (UD) is a logical unit of nodes. During Service Fabric orchestrated upgrades (either an application upgrade or a cluster upgrade), all nodes in a UD are taken down to perform the upgrade while nodes in other UDs remain available to serve requests. The firmware upgrades you perform on your machines do not honor UDs, so you must do them one machine at a time.

The simplest way to think about these concepts is to consider FDs as the unit of unplanned failure and UDs as the unit of planned maintenance.

When you specify UDs in ClusterConfig.json, you can choose the name for each UD. For example, the following names are valid:

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Blue"

For more detailed information on upgrade domains and fault domains, see [Describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md).

### <a name="step-5-download-the-service-fabric-standalone-package-for-windows-server"></a>Step 5: Download the Service Fabric standalone package for Windows Server
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) and unzip the package, either to a deployment machine that is not part of the cluster, or to one of the machines that will be a part of your cluster.

### <a name="step-6-modify-cluster-configuration"></a>Step 6: Modify cluster configuration
To create a standalone cluster you have to create a standalone cluster configuration ClusterConfig.json file, which describes the specification of the cluster. You can base the configuration file on the templates found at the below link. <br>
[Standalone Cluster Configurations](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

For details on the sections in this file, see [Configuration settings for standalone Windows cluster](service-fabric-cluster-manifest.md).

Open one of the ClusterConfig.json files from the package you downloaded and modify the following settings:
| **Configuration Setting** | **Description** |
| --- | --- |
| **NodeTypes** |Node types allow you to separate your cluster nodes into various groups. A cluster must have at least one NodeType. All nodes in a group have the following common characteristics: <br> **Name** - This is the node type name. <br>**Endpoint Ports** - These are various named end points (ports) that are associated with this node type. You can use any port number that you wish, as long as they do not conflict with anything else in this manifest and are not already in use by any other application running on the machine/VM. <br> **Placement Properties** - These describe properties for this node type that you use as placement constraints for the system services or your services. These properties are user-defined key/value pairs that provide extra meta data for a given node. Examples of node properties would be whether the node has a hard drive or graphics card, the number of spindles in its hard drive, cores, and other physical properties. <br> **Capacities** - Node capacities define the name and amount of a particular resource that a particular node has available for consumption. For example, a node may define that it has capacity for a metric called “MemoryInMb” and that it has 2048 MB available by default. These capacities are used at runtime to ensure that services that require particular amounts of resources are placed on the nodes that have those resources available in the required amounts.<br>**IsPrimary** - If you have more than one NodeType defined ensure that only one is set to primary with the value *true*, which is where the system services run. All other node types should be set to the value *false* |
| **Nodes** |These are the details for each of the nodes that are part of the cluster (node type, node name, IP address, fault domain, and upgrade domain of the node). The machines you want the cluster to be created on need to be listed here with their IP addresses. <br> If you use the same IP address for all the nodes, then a one-box cluster is created, which you can use for testing purposes. Do not use One-box clusters for deploying production workloads. |

After the cluster configuration has had all settings configured to the environment, it can be tested against the cluster environment (step 7).

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>Step 7. Environment setup

When a cluster administrator configures a Service Fabric standalone cluster, the environment is needs to be set up with the following criteria: <br>
1. The user creating the cluster should have administrator-level security privileges to all machines that are listed as nodes in the cluster configuration file.
2. Machine from which the cluster is created, as well as each cluster node machine must:
* Have Service Fabric SDK uninstalled
* Have Service Fabric runtime uninstalled 
* Have the Windows Firewall service (mpssvc) enabled
* Have the Remote Registry Service (remoteregistry) enabled
* Have file sharing (SMB) enabled
* Have necessary ports opened, based on cluster configuration ports
* Have necessary ports opened for Windows SMB and Remote Registry service: 135, 137, 138, 139, and 445
* Have network connectivity to one another
3. None of the cluster node machines should be a Domain Controller.
4. If the cluster to be deployed is a secure cluster, validate the necessary security prerequisites are in place, and are configured correctly against the configuration.
5. If the cluster machines are not internet-accessible, set the following in the cluster configuration:
* Disable telemetry:   Under *properties* set   *"enableTelemetry": false*
* Disable automatic Fabric version downloading & notifications that the current cluster version is nearing end of support:   Under *properties* set   *"fabricClusterAutoupgradeEnabled": false*
* Alternatively if network internet access is limited to white-listed domains, the domains below are required for automatic upgrade:   go.microsoft.com   download.microsoft.com

6. Set appropriate Service Fabric antivirus exclusions:

| **Antivirus Excluded directories** |
| --- |
| Program Files\Microsoft Service Fabric |
| FabricDataRoot (from cluster configuration) |
| FabricLogRoot (from cluster configuration) |

| **Antivirus Excluded processes** |
| --- |
| Fabric.exe |
| FabricHost.exe |
| FabricInstallerService.exe |
| FabricSetup.exe |
| FabricDeployer.exe |
| ImageBuilder.exe |
| FabricGateway.exe |
| FabricDCA.exe |
| FabricFAS.exe |
| FabricUOS.exe |
| FabricRM.exe |
| FileStoreService.exe |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a>Step 8. Validate environment using TestConfiguration script
The TestConfiguration.ps1 script can be found in the standalone package. It is used as a Best Practices Analyzer to validate some of the criteria above and should be used as a sanity check to validate whether a cluster can be deployed on a given environment. If there is any failure, refer to the list under [Environment Setup](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting. 

This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file. The machine that this script is run on does not have to be part of the cluster.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
Running Best Practices Analyzer...
Best Practices Analyzer completed successfully.


LocalAdminPrivilege        : True
IsJsonValid                : True
IsCabValid                 : True
RequiredPortsOpen          : True
RemoteRegistryAvailable    : True
FirewallAvailable          : True
RpcCheckPassed             : True
NoConflictingInstallations : True
FabricInstallable          : True
Passed                     : True
```

Currently this configuration testing module does not validate the security configuration so this has to be done independently.  

> [!NOTE]
> We are continually making improvements to make this module more robust, so if there is a faulty or missing case which you believe isn't currently caught by TestConfiguration, please let us know through our [support channels](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).   
> 
> 

## <a name="next-steps"></a>Next steps
* [Create a standalone cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md)
