---
title: How Cloud Foundry Integrates with Azure | Microsoft Docs
description: Describes how Cloud Foundry can utlize Azure services to enhance the Enterprice experience
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
ms.date: 05/11/2018
ms.author: ningk
ms.openlocfilehash: 689730edcc98a23c82373ae8d36c3b831b33c076
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868480"
---
# <a name="integrate-cloud-foundry-with-azure"></a>Integrate Cloud Foundry with Azure

[Cloud Foundry](https://docs.cloudfoundry.org/) is a PaaS platform running on top of cloud providers’ IaaS platform. It offers consistent application deployment experience across cloud providers. In addition, it can also integrate with various Azure services, with enterprise grade HA, scalability, and cost savings.
There are [6 subsystems of Cloud Foundry](https://docs.cloudfoundry.org/concepts/architecture/),  that can be flexibly scale online, including: Routing, Authentication, Application life cycle management, Service management, Messaging and Monitoring. For each of the subsystems, you can configure Cloud Foundry to utilize correspondent Azure service. 

![Cloud Foundry on Azure Integration Architecture](media/CFOnAzureEcosystem-colored.png)

## <a name="1-high-availability-and-scalability"></a>1. High Availability and Scalability
### <a name="managed-disk"></a>Managed Disk
Bosh utilizes Azure CPI (Cloud Provider Interface) for disk creating and deleting routines. By default, unmanaged disks are used. It requires customer to manually create storage accounts,    then configure the accounts in CF manifest files. This is due to the limitation on the number of disks per storage account.
Now [Managed Disk](https://azure.microsoft.com/services/managed-disks/) is available, offers managed secure and reliable disk storage for virtual machines. Customer no longer need to deal with the storage account for scale and HA. Azure arranges disks automatically. Whether it is a new or an existing deployment, the Azure CPI will handle the creation or migration of the managed disk during a CF deployment. It is supported with PCF 1.11. You can also explore the open-source Cloud Foundry [Managed Disk guidance](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs/advanced/managed-disks) for reference. 
### <a name="availability-zone-"></a>Availability Zone *
As a cloud-native application platform, Cloud Foundry is designed with [four level of High availability](https://docs.pivotal.io/pivotalcf/2-1/concepts/high-availability.html). While the first three levels of software failures can be handled by CF system itself, platform fault tolerance is provided by cloud providers. The key CF components should be protected with a cloud provider’s platform HA solution. This includes GoRouters, Diego Brains, CF database and service tiles. By default, [Azure Availability Set](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs/advanced/deploy-cloudfoundry-with-availability-sets) is used for fault tolerance between clusters in a data center.
The good new is, [Azure Availability Zone](https://docs.microsoft.com/azure/availability-zones/az-overview ) is released now, bringing the fault tolerance to next level, with low latency redundancy across data centers.
Azure Availability Zone achieves HA by placing a set of VMs into 2+ data centers, each set of VMs are redundant to other sets. If one Zone is down, the other sets are still live, isolated from the disaster.
> [!NOTE] 
> Azure Availability Zone is not offered to all regions yet, check the latest [announcement for the list of supported regions](https://docs.microsoft.com/azure/availability-zones/az-overview). For Open Source Cloud Foundry, check [Azure Availability Zone for open source Cloud Foundry guidance](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs/advanced/availability-zone).

## <a name="2-network-routing"></a>2. Network Routing
By default, Azure basic load balancer is used for incoming CF API/apps requests, forwarding them to the Gorouters. CF components like Diego Brain, MySQL, ERT can also use the load balancer to balance the traffic for HA. In addition, Azure provides a set of fully managed load balancing solutions. If you are looking for TLS termination ("SSL offload") or per HTTP/HTTPS request application layer processing, consider Application Gateway. For high availability and scalability load balancing on layer 4, consider standard load balancer.
### <a name="azure-application-gateway-"></a>Azure Application Gateway *
[Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) offers various layer 7 load balancing capabilities, including SSL offloading, end to end SSL, Web Application Firewall, cookie-based session affinity and more. You can [configure Application Gateway in Open Source Cloud Foundry](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs/advanced/application-gateway). For PCF, check the  [PCF 2.1 release notes](https://docs.pivotal.io/pivotalcf/2-1/pcf-release-notes/opsmanager-rn.html#azure-application-gateway) for POC test.

### <a name="azure-standard-load-balancer-"></a>Azure Standard Load Balancer *
Azure Load Balancer is a Layer 4 load balancer. It is used to distribute the traffic among instances of services in a load-balanced set. The standard version provides [advanced features](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) on top of the basic version. For example 1. The backend pool max limit is raised from 100 to 1000 VMs.  2. The endpoints now support multiple availability sets instead of single availability set.  3. Additional features like HA ports, richer monitoring data, etc. If you are moving to Azure Availability Zone, standard load balancer is required. For a new deployment, we recommend you to start with Azure Standard Load Balancer. 

## <a name="3-authentication"></a>3. Authentication 
[Cloud Foundry User Account and Authentication](https://docs.cloudfoundry.org/concepts/architecture/uaa.html) is the central identity management service for CF and its various components. [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) is Microsoft’s multi-tenant, cloud-based directory and identity management service. By default, UAA is used for Cloud Foundry authentication. As an advanced option, UAA also supports Azure AD as an external user store. Azure AD users can access Cloud Foundry using their LDAP identity, without a Cloud Foundry account. Follow these steps to [configure the Azure AD for UAA in PCF](http://docs.pivotal.io/p-identity/1-6/azure/index.html).

## <a name="4-data-storage-for-cloud-foundry-runtime-system"></a>4. Data storage for Cloud Foundry Runtime System
Cloud Foundry offers great extensibility to use Azure blobstore or Azure MySQL/PostgreSQL services for application runtime system storage.
### <a name="azure-blobstore-for-cloud-foundry-cloud-controller-blobstore"></a>Azure Blobstore for Cloud Foundry Cloud Controller blobstore
The Cloud Controller blobstore is a critical data store for buildpacks, droplets, packages, and resource pools. By default, NFS server is used for Cloud Controller blobstore. To avoid single point of failure, use Azure Blob Storage as external store. Check out the [Cloud Foundry documentation](https://docs.cloudfoundry.org/deploying/common/cc-blobstore-config.html) for background, and [options in Pivotal Cloud Foundry](https://docs.pivotal.io/pivotalcf/2-0/customizing/azure.html).

### <a name="mysqlpostgresql-as-cloud-foundry-elastic-run-time-database-"></a>MySQL/PostgreSQL as Cloud Foundry Elastic Run Time Database *
CF Elastic Runtime requires two major system databases:
#### <a name="ccdb"></a>CCDB 
The Cloud Controller database.  Cloud Controller provides REST API endpoints for clients to access the system. CCDB stores tables for orgs, spaces, services, user roles, and more for Cloud controller.
#### <a name="uaadb"></a>UAADB 
The database for User Account and Authentication. It stores the user authentication related data, for example encrypted user names and passwords.

By default, a local system database (MySQL) can be used. For HA and to scale, leverage Azure managed MySQL or PostgreSQL services. Here is the instruction of [enabling Azure MySQL/PostgreSQL for CCDB, UAADB and other system databases with Open Source Cloud Foundry](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs/advanced/configure-cf-external-databases-using-azure-mysql-postgres-service).

## <a name="5-open-service-broker"></a>5. Open Service Broker
Azure service broker offers consistent interface to manage application’s access to Azure services. The new [Open Service Broker for Azure project](https://github.com/Azure/open-service-broker-azure) provides a single and simple way to deliver services to applications across Cloud Foundry, OpenShift, and Kubernetes. See the [Azure Open Service Broker for PCF tile](https://network.pivotal.io/products/azure-open-service-broker-pcf/) for deployment instructions on PCF.

## <a name="6-metrics-and-logging"></a>6. Metrics and Logging
The Azure Log Analytics Nozzle is a Cloud Foundry component, that forwards metrics from the [Cloud Foundry loggregator firehose](https://docs.cloudfoundry.org/loggregator/architecture.html) to [Azure Log Analytics](https://azure.microsoft.com/services/log-analytics/). With the Nozzle, you can collect, view, and analyze your CF system health and performance metrics across multiple deployments.
Click [here](https://docs.microsoft.com/azure/cloudfoundry/cloudfoundry-oms-nozzle) to learn how to deploy the Azure Log Analytics Nozzle to both Open Source and Pivotal Cloud Foundry environment, and then access the data from the Azure Log Analytics OMS console. 
> [!NOTE]
> From PCF 2.0, BOSH health metrics for VMs are forwarded to the Loggregator Firehose by default, and are integrated into Azure Log Analytics OMS console.

## <a name="7-cost-saving"></a>7. Cost Saving
### <a name="cost-saving-for-devtest-environments"></a>Cost Saving for Dev/Test Environments
#### <a name="b-series-"></a>B-Series: *
While F and D VM series were commonly recommended for Pivotal Cloud Foundry production environment, the new “burstable” [B-series](https://azure.microsoft.com/blog/introducing-b-series-our-new-burstable-vm-size/) brings new options. The B-series burstable VMs are ideal for workloads that do not need the full performance of the CPU continuously, like web servers, small databases and development and test environments. These workloads typically have burstable performance requirements. It is $0.012/hour (B1) compared to $0.05/hour (F1), see the full list of [VM sizes](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general) and [prices](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) for details. 
#### <a name="managed-standard-disk"></a>Managed Standard Disk: 
Premium disks were recommended for reliable performance in production.  With [Managed Disk](https://azure.microsoft.com/services/managed-disks/), standard storage can also deliver similar reliability, with different performance. For workload that is not performance-sensitive, like dev/Test or non-critical environment, managed standard disks offer an alternative option with lower cost.  
### <a name="cost-saving-in-general"></a>Cost saving in General 
#### <a name="significant-vm-cost-saving-with-azure-reservations"></a>Significant VM Cost Saving with Azure reservations: 
Today all CF VMs are billed using “on-demand” pricing, even though the environments typically stay up indefinitely. Now you can reserve VM capacity on a 1 or 3-year term, and gain discounts of 45-65%. Discounts are applied in the billing system, with no changes to your environment. For details, see [How Azure reservations works](https://azure.microsoft.com/pricing/reserved-vm-instances/). 
#### <a name="managed-premium-disk-with-smaller-sizes"></a>Managed Premium Disk with Smaller Sizes: 
Managed disks support smaller disk sizes, for example P4(32 GB) and P6(64 GB) for both premium and standard disks. If you have small workloads, you can save cost when migrating from standard premium disks to managed premium disks.
#### <a name="utilizing-azure-first-party-services"></a>Utilizing Azure First Party Services: 
Taking advantage of Azure’s first party service will lower the long-term administration cost, in addition to HA and reliability mentioned in above sections. 

Pivotal has launched a [Small Footprint ERT](https://docs.pivotal.io/pivotalcf/2-0/customizing/small-footprint.html) for PCF customers, the components are co-located into just 4 VMs, running up to 2500 application instances. The trial version is now available through [Azure Market place](https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry).

## <a name="next-steps"></a>Next Steps
Azure integration features are first available with [Open Source Cloud Foundry](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs/advanced/), before it is available on Pivotal Cloud Foundry. Features marked with * are still not available through PCF. Cloud Foundry integration with Azure Stack is not covered in this document either.
For PCF support on the features marked with *, or Cloud Foundry integration with Azure Stack, contact your Pivotal and Microsoft account manager for latest status. 
