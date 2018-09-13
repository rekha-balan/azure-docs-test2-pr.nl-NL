---
title: Multi-Tenant Web Application Pattern | Microsoft Docs
description: Find architectural overviews and design patterns that describe how to implement a multi-tenant web application on Azure.
services: ''
documentationcenter: .net
author: wadepickett
manager: wpickett
editor: ''
ms.assetid: 4f0281d2-1555-42b0-a99d-1222fade0b0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2015
ms.author: wpickett
ms.openlocfilehash: c1614eeac922a4fc496be77b4d1d1588f28b4284
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554931"
---
# <a name="multitenant-applications-in-azure"></a><span data-ttu-id="b12ce-103">Multitenant Applications in Azure</span><span class="sxs-lookup"><span data-stu-id="b12ce-103">Multitenant Applications in Azure</span></span>
<span data-ttu-id="b12ce-104">A multitenant application is a shared resource that allows separate users, or "tenants," to view the application as though it was their own.</span><span class="sxs-lookup"><span data-stu-id="b12ce-104">A multitenant application is a shared resource that allows separate users, or "tenants," to view the application as though it was their own.</span></span> <span data-ttu-id="b12ce-105">A typical scenario that lends itself to a multitenant application is one in which all users of the application may wish to customize the user experience but otherwise have the same basic business requirements.</span><span class="sxs-lookup"><span data-stu-id="b12ce-105">A typical scenario that lends itself to a multitenant application is one in which all users of the application may wish to customize the user experience but otherwise have the same basic business requirements.</span></span> <span data-ttu-id="b12ce-106">Examples of large multitenant applications are Office 365, Outlook.com, and visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="b12ce-106">Examples of large multitenant applications are Office 365, Outlook.com, and visualstudio.com.</span></span>

<span data-ttu-id="b12ce-107">From an application provider's perspective, the benefits of multitenancy mostly relate to operational and cost efficiencies.</span><span class="sxs-lookup"><span data-stu-id="b12ce-107">From an application provider's perspective, the benefits of multitenancy mostly relate to operational and cost efficiencies.</span></span> <span data-ttu-id="b12ce-108">One version of your application can meet the needs of many tenants/customers, allowing consolidation of system administration tasks such as monitoring, performance tuning, software maintenance, and data backups.</span><span class="sxs-lookup"><span data-stu-id="b12ce-108">One version of your application can meet the needs of many tenants/customers, allowing consolidation of system administration tasks such as monitoring, performance tuning, software maintenance, and data backups.</span></span>

<span data-ttu-id="b12ce-109">The following provides a list of the most significant goals and requirements from a provider's perspective.</span><span class="sxs-lookup"><span data-stu-id="b12ce-109">The following provides a list of the most significant goals and requirements from a provider's perspective.</span></span>

* <span data-ttu-id="b12ce-110">**Provisioning**: You must be able to provision new tenants for the application.</span><span class="sxs-lookup"><span data-stu-id="b12ce-110">**Provisioning**: You must be able to provision new tenants for the application.</span></span>  <span data-ttu-id="b12ce-111">For multitenant applications with a large number of tenants, it is usually necessary to automate this process by enabling self-service provisioning.</span><span class="sxs-lookup"><span data-stu-id="b12ce-111">For multitenant applications with a large number of tenants, it is usually necessary to automate this process by enabling self-service provisioning.</span></span>
* <span data-ttu-id="b12ce-112">**Maintainability**: You must be able to upgrade the application and perform other maintenance tasks while multiple tenants are using it.</span><span class="sxs-lookup"><span data-stu-id="b12ce-112">**Maintainability**: You must be able to upgrade the application and perform other maintenance tasks while multiple tenants are using it.</span></span>
* <span data-ttu-id="b12ce-113">**Monitoring**: You must be able to monitor the application at all times to identify any problems and to troubleshoot them.</span><span class="sxs-lookup"><span data-stu-id="b12ce-113">**Monitoring**: You must be able to monitor the application at all times to identify any problems and to troubleshoot them.</span></span> <span data-ttu-id="b12ce-114">This includes monitoring how each tenant is using the application.</span><span class="sxs-lookup"><span data-stu-id="b12ce-114">This includes monitoring how each tenant is using the application.</span></span>

<span data-ttu-id="b12ce-115">A properly implemented multitenant application provides the following benefits to users.</span><span class="sxs-lookup"><span data-stu-id="b12ce-115">A properly implemented multitenant application provides the following benefits to users.</span></span>

* <span data-ttu-id="b12ce-116">**Isolation**: The activities of individual tenants do not affect the use of the application by other tenants.</span><span class="sxs-lookup"><span data-stu-id="b12ce-116">**Isolation**: The activities of individual tenants do not affect the use of the application by other tenants.</span></span> <span data-ttu-id="b12ce-117">Tenants cannot access each other's data.</span><span class="sxs-lookup"><span data-stu-id="b12ce-117">Tenants cannot access each other's data.</span></span> <span data-ttu-id="b12ce-118">It appears to the tenant as though they have exclusive use of the application.</span><span class="sxs-lookup"><span data-stu-id="b12ce-118">It appears to the tenant as though they have exclusive use of the application.</span></span>
* <span data-ttu-id="b12ce-119">**Availability**: Individual tenants want the application to be constantly available, perhaps with guarantees defined in an SLA.</span><span class="sxs-lookup"><span data-stu-id="b12ce-119">**Availability**: Individual tenants want the application to be constantly available, perhaps with guarantees defined in an SLA.</span></span> <span data-ttu-id="b12ce-120">Again, the activities of other tenants should not affect the availability of the application.</span><span class="sxs-lookup"><span data-stu-id="b12ce-120">Again, the activities of other tenants should not affect the availability of the application.</span></span>
* <span data-ttu-id="b12ce-121">**Scalability**: The application scales to meet the demand of individual tenants.</span><span class="sxs-lookup"><span data-stu-id="b12ce-121">**Scalability**: The application scales to meet the demand of individual tenants.</span></span> <span data-ttu-id="b12ce-122">The presence and actions of other tenants should not affect the performance of the application.</span><span class="sxs-lookup"><span data-stu-id="b12ce-122">The presence and actions of other tenants should not affect the performance of the application.</span></span>
* <span data-ttu-id="b12ce-123">**Costs**: Costs are lower than running a dedicated, single-tenant application because multi-tenancy enables the sharing of resources.</span><span class="sxs-lookup"><span data-stu-id="b12ce-123">**Costs**: Costs are lower than running a dedicated, single-tenant application because multi-tenancy enables the sharing of resources.</span></span>
* <span data-ttu-id="b12ce-124">**Customizability**.</span><span class="sxs-lookup"><span data-stu-id="b12ce-124">**Customizability**.</span></span> <span data-ttu-id="b12ce-125">The ability to customize the application for an individual tenant in various ways such as adding or removing features, changing colors and logos, or even adding their own code or script.</span><span class="sxs-lookup"><span data-stu-id="b12ce-125">The ability to customize the application for an individual tenant in various ways such as adding or removing features, changing colors and logos, or even adding their own code or script.</span></span>

<span data-ttu-id="b12ce-126">In short, while there are many considerations that you must take into account to provide a highly scalable service, there are also a number of the goals and requirements that are common to many multitenant applications.</span><span class="sxs-lookup"><span data-stu-id="b12ce-126">In short, while there are many considerations that you must take into account to provide a highly scalable service, there are also a number of the goals and requirements that are common to many multitenant applications.</span></span> <span data-ttu-id="b12ce-127">Some may not be relevant in specific scenarios, and the importance of individual goals and requirements will differ in each scenario.</span><span class="sxs-lookup"><span data-stu-id="b12ce-127">Some may not be relevant in specific scenarios, and the importance of individual goals and requirements will differ in each scenario.</span></span> <span data-ttu-id="b12ce-128">As a provider of the multitenant application, you will also have goals and requirements such as, meeting the tenants' goals and requirements, profitability, billing, multiple service levels, provisioning, maintainability monitoring, and automation.</span><span class="sxs-lookup"><span data-stu-id="b12ce-128">As a provider of the multitenant application, you will also have goals and requirements such as, meeting the tenants' goals and requirements, profitability, billing, multiple service levels, provisioning, maintainability monitoring, and automation.</span></span>

<span data-ttu-id="b12ce-129">For more information on additional design considerations of a multitenant application, see [Hosting a Multi-Tenant Application on Azure][Hosting a Multi-Tenant Application on Azure].</span><span class="sxs-lookup"><span data-stu-id="b12ce-129">For more information on additional design considerations of a multitenant application, see [Hosting a Multi-Tenant Application on Azure][Hosting a Multi-Tenant Application on Azure].</span></span> <span data-ttu-id="b12ce-130">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="b12ce-130">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span> 

<span data-ttu-id="b12ce-131">Azure provides many features that allow you to address the key problems encountered when designing a multitenant system.</span><span class="sxs-lookup"><span data-stu-id="b12ce-131">Azure provides many features that allow you to address the key problems encountered when designing a multitenant system.</span></span>

<span data-ttu-id="b12ce-132">**Isolation**</span><span class="sxs-lookup"><span data-stu-id="b12ce-132">**Isolation**</span></span>

* <span data-ttu-id="b12ce-133">Segment Website Tenants by Host Headers with or without SSL communication</span><span class="sxs-lookup"><span data-stu-id="b12ce-133">Segment Website Tenants by Host Headers with or without SSL communication</span></span>
* <span data-ttu-id="b12ce-134">Segment Website Tenants by Query Parameters</span><span class="sxs-lookup"><span data-stu-id="b12ce-134">Segment Website Tenants by Query Parameters</span></span>
* <span data-ttu-id="b12ce-135">Web Services in Worker Roles</span><span class="sxs-lookup"><span data-stu-id="b12ce-135">Web Services in Worker Roles</span></span>
  * <span data-ttu-id="b12ce-136">Worker Roles.</span><span class="sxs-lookup"><span data-stu-id="b12ce-136">Worker Roles.</span></span> <span data-ttu-id="b12ce-137">that typically process data on the backend of an application.</span><span class="sxs-lookup"><span data-stu-id="b12ce-137">that typically process data on the backend of an application.</span></span>
  * <span data-ttu-id="b12ce-138">Web Roles that typically act as the frontend for applications.</span><span class="sxs-lookup"><span data-stu-id="b12ce-138">Web Roles that typically act as the frontend for applications.</span></span>

<span data-ttu-id="b12ce-139">**Storage**</span><span class="sxs-lookup"><span data-stu-id="b12ce-139">**Storage**</span></span>

<span data-ttu-id="b12ce-140">Data management such as Azure SQL Database or Azure Storage services such as the Table service which provides services for storage of large amounts of unstructured data and the Blob service which provides services to store large amounts of unstructured text or binary data such as video, audio and images.</span><span class="sxs-lookup"><span data-stu-id="b12ce-140">Data management such as Azure SQL Database or Azure Storage services such as the Table service which provides services for storage of large amounts of unstructured data and the Blob service which provides services to store large amounts of unstructured text or binary data such as video, audio and images.</span></span>

* <span data-ttu-id="b12ce-141">Securing Multitenant Data in SQL Database appropriate per-tenant SQL Server logins.</span><span class="sxs-lookup"><span data-stu-id="b12ce-141">Securing Multitenant Data in SQL Database appropriate per-tenant SQL Server logins.</span></span>
* <span data-ttu-id="b12ce-142">Using Azure Tables for Application Resources By specifying a container level access policy, you can the ability to adjust permissions without having to issue new URL's for the resources protected with shared access signatures.</span><span class="sxs-lookup"><span data-stu-id="b12ce-142">Using Azure Tables for Application Resources By specifying a container level access policy, you can the ability to adjust permissions without having to issue new URL's for the resources protected with shared access signatures.</span></span>
* <span data-ttu-id="b12ce-143">Azure Queues for Application Resources Azure queues are commonly used to drive processing on behalf of tenants, but may also be used to distribute work required for provisioning or management.</span><span class="sxs-lookup"><span data-stu-id="b12ce-143">Azure Queues for Application Resources Azure queues are commonly used to drive processing on behalf of tenants, but may also be used to distribute work required for provisioning or management.</span></span>
* <span data-ttu-id="b12ce-144">Service Bus Queues for Application Resources that pushes work to a shared a service, you can use a single queue where each tenant sender only has permissions (as derived from claims issued from ACS) to push to that queue, while only the receivers from the service have permission to pull from the queue the data coming from multiple tenants.</span><span class="sxs-lookup"><span data-stu-id="b12ce-144">Service Bus Queues for Application Resources that pushes work to a shared a service, you can use a single queue where each tenant sender only has permissions (as derived from claims issued from ACS) to push to that queue, while only the receivers from the service have permission to pull from the queue the data coming from multiple tenants.</span></span>

<span data-ttu-id="b12ce-145">**Connection and Security Services**</span><span class="sxs-lookup"><span data-stu-id="b12ce-145">**Connection and Security Services**</span></span>

* <span data-ttu-id="b12ce-146">Azure Service Bus, a messaging infrastructure that sits between applications allowing them to exchange messages in a loosely coupled way for improved scale and resiliency.</span><span class="sxs-lookup"><span data-stu-id="b12ce-146">Azure Service Bus, a messaging infrastructure that sits between applications allowing them to exchange messages in a loosely coupled way for improved scale and resiliency.</span></span>

<span data-ttu-id="b12ce-147">**Networking Services**</span><span class="sxs-lookup"><span data-stu-id="b12ce-147">**Networking Services**</span></span>

<span data-ttu-id="b12ce-148">Azure provides several networking services that support authentication, and improve manageability of your hosted applications.</span><span class="sxs-lookup"><span data-stu-id="b12ce-148">Azure provides several networking services that support authentication, and improve manageability of your hosted applications.</span></span> <span data-ttu-id="b12ce-149">These services include the following:</span><span class="sxs-lookup"><span data-stu-id="b12ce-149">These services include the following:</span></span>

* <span data-ttu-id="b12ce-150">Azure Virtual Network lets you provision and manage virtual private networks (VPNs) in Azure as well as securely link these with on-premises IT infrastructure.</span><span class="sxs-lookup"><span data-stu-id="b12ce-150">Azure Virtual Network lets you provision and manage virtual private networks (VPNs) in Azure as well as securely link these with on-premises IT infrastructure.</span></span>
* <span data-ttu-id="b12ce-151">Virtual Network Traffic Manager allows you to load balance incoming traffic across multiple hosted Azure services whether they're running in the same datacenter or across different datacenters around the world.</span><span class="sxs-lookup"><span data-stu-id="b12ce-151">Virtual Network Traffic Manager allows you to load balance incoming traffic across multiple hosted Azure services whether they're running in the same datacenter or across different datacenters around the world.</span></span>
* <span data-ttu-id="b12ce-152">Azure Active Directory (Azure AD) is a modern, REST-based service that provides identity management and access control capabilities for your cloud applications.</span><span class="sxs-lookup"><span data-stu-id="b12ce-152">Azure Active Directory (Azure AD) is a modern, REST-based service that provides identity management and access control capabilities for your cloud applications.</span></span> <span data-ttu-id="b12ce-153">Using Azure AD for Application Resources Azure AD to provides an easy way of authenticating and authorizing users to gain access to your web applications and services while allowing the features of authentication and authorization to be factored out of your code.</span><span class="sxs-lookup"><span data-stu-id="b12ce-153">Using Azure AD for Application Resources Azure AD to provides an easy way of authenticating and authorizing users to gain access to your web applications and services while allowing the features of authentication and authorization to be factored out of your code.</span></span>
* <span data-ttu-id="b12ce-154">Azure Service Bus provides a secure messaging and data flow capability for distributed and hybrid applications, such as communication between Azure hosted applications and on-premises applications and services, without requiring complex firewall and security infrastructures.</span><span class="sxs-lookup"><span data-stu-id="b12ce-154">Azure Service Bus provides a secure messaging and data flow capability for distributed and hybrid applications, such as communication between Azure hosted applications and on-premises applications and services, without requiring complex firewall and security infrastructures.</span></span> <span data-ttu-id="b12ce-155">Using Service Bus Relay for Application Resources to The services that are exposed as endpoints may belong to the tenant (for example, hosted outside of the system, such as on-premise), or they may be services provisioned specifically for the tenant (because sensitive, tenant-specific data travels across them).</span><span class="sxs-lookup"><span data-stu-id="b12ce-155">Using Service Bus Relay for Application Resources to The services that are exposed as endpoints may belong to the tenant (for example, hosted outside of the system, such as on-premise), or they may be services provisioned specifically for the tenant (because sensitive, tenant-specific data travels across them).</span></span>

<span data-ttu-id="b12ce-156">**Provisioning Resources**</span><span class="sxs-lookup"><span data-stu-id="b12ce-156">**Provisioning Resources**</span></span>

<span data-ttu-id="b12ce-157">Azure provides a number of ways provision new tenants for the application.</span><span class="sxs-lookup"><span data-stu-id="b12ce-157">Azure provides a number of ways provision new tenants for the application.</span></span> <span data-ttu-id="b12ce-158">For multitenant applications with a large number of tenants, it is usually necessary to automate this process by enabling self-service provisioning.</span><span class="sxs-lookup"><span data-stu-id="b12ce-158">For multitenant applications with a large number of tenants, it is usually necessary to automate this process by enabling self-service provisioning.</span></span>

* <span data-ttu-id="b12ce-159">Worker roles allow you to provision and de-provision per tenant resources (such as when a new tenant signs-up or cancels), collect metrics for metering use, and manage scale following a certain schedule or in response to the crossing of thresholds of key performance indicators.</span><span class="sxs-lookup"><span data-stu-id="b12ce-159">Worker roles allow you to provision and de-provision per tenant resources (such as when a new tenant signs-up or cancels), collect metrics for metering use, and manage scale following a certain schedule or in response to the crossing of thresholds of key performance indicators.</span></span> <span data-ttu-id="b12ce-160">This same role may also be used to push out updates and upgrades to the solution.</span><span class="sxs-lookup"><span data-stu-id="b12ce-160">This same role may also be used to push out updates and upgrades to the solution.</span></span>
* <span data-ttu-id="b12ce-161">Azure Blobs can be used to provision compute or pre-initialized storage resources for new tenants while providing container level access policies to protect the compute service Packages, VHD images and other resources.</span><span class="sxs-lookup"><span data-stu-id="b12ce-161">Azure Blobs can be used to provision compute or pre-initialized storage resources for new tenants while providing container level access policies to protect the compute service Packages, VHD images and other resources.</span></span>
* <span data-ttu-id="b12ce-162">Options for provisioning SQL Database resources for a tenant include:</span><span class="sxs-lookup"><span data-stu-id="b12ce-162">Options for provisioning SQL Database resources for a tenant include:</span></span>
  
  * <span data-ttu-id="b12ce-163">DDL in scripts or embedded as resources within assemblies</span><span class="sxs-lookup"><span data-stu-id="b12ce-163">DDL in scripts or embedded as resources within assemblies</span></span>
  * <span data-ttu-id="b12ce-164">SQL Server 2008 R2 DAC Packages deployed programmatically.</span><span class="sxs-lookup"><span data-stu-id="b12ce-164">SQL Server 2008 R2 DAC Packages deployed programmatically.</span></span>
  * <span data-ttu-id="b12ce-165">Copying from a master reference database</span><span class="sxs-lookup"><span data-stu-id="b12ce-165">Copying from a master reference database</span></span>
  * <span data-ttu-id="b12ce-166">Using database Import and Export to provision new databases from a file.</span><span class="sxs-lookup"><span data-stu-id="b12ce-166">Using database Import and Export to provision new databases from a file.</span></span>

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716