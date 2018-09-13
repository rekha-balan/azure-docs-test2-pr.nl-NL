---
title: Install Azure AD Connect using SQL delegated administrator permissions | Microsoft Docs
description: This topic describes an update to Azure AD Connect that allows for installation using an account that only has SQL dbo permissions.
documentationcenter: ''
author: billmath
manager: mtillman
editor: ''
ms.reviewer: jparsons
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 198ecdbf81c2b8efeec23da2c5d5d087128b20e9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867827"
---
# <a name="install-azure-ad-connect-using-sql-delegated-administrator-permissions"></a><span data-ttu-id="ade1f-103">Install Azure AD Connect using SQL delegated administrator permissions</span><span class="sxs-lookup"><span data-stu-id="ade1f-103">Install Azure AD Connect using SQL delegated administrator permissions</span></span>
<span data-ttu-id="ade1f-104">Prior to the latest Azure AD Connect build, administrative delegation, when deploying configurations that required SQL, was not supported.</span><span class="sxs-lookup"><span data-stu-id="ade1f-104">Prior to the latest Azure AD Connect build, administrative delegation, when deploying configurations that required SQL, was not supported.</span></span>  <span data-ttu-id="ade1f-105">Users who wanted to install Azure AD Connect needed to have server administrator (SA) permissions on the SQL server.</span><span class="sxs-lookup"><span data-stu-id="ade1f-105">Users who wanted to install Azure AD Connect needed to have server administrator (SA) permissions on the SQL server.</span></span>

<span data-ttu-id="ade1f-106">With the latest release of Azure AD Connect, provisioning the database can now be performed out of band by the SQL administrator and then installed by the Azure AD Connect administrator with database owner rights.</span><span class="sxs-lookup"><span data-stu-id="ade1f-106">With the latest release of Azure AD Connect, provisioning the database can now be performed out of band by the SQL administrator and then installed by the Azure AD Connect administrator with database owner rights.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ade1f-107">Before you begin</span><span class="sxs-lookup"><span data-stu-id="ade1f-107">Before you begin</span></span>
<span data-ttu-id="ade1f-108">To use this feature, you need to realize that there are several moving parts and each one may involve a different administrator in your organization.</span><span class="sxs-lookup"><span data-stu-id="ade1f-108">To use this feature, you need to realize that there are several moving parts and each one may involve a different administrator in your organization.</span></span>  <span data-ttu-id="ade1f-109">The following table summarizes the individual roles and their respective duties in deploying Azure AD Connect with this feature.</span><span class="sxs-lookup"><span data-stu-id="ade1f-109">The following table summarizes the individual roles and their respective duties in deploying Azure AD Connect with this feature.</span></span>

|<span data-ttu-id="ade1f-110">Role</span><span class="sxs-lookup"><span data-stu-id="ade1f-110">Role</span></span>|<span data-ttu-id="ade1f-111">Description</span><span class="sxs-lookup"><span data-stu-id="ade1f-111">Description</span></span>|
|-----|-----|
|<span data-ttu-id="ade1f-112">Domain or Forest AD administrator</span><span class="sxs-lookup"><span data-stu-id="ade1f-112">Domain or Forest AD administrator</span></span>|<span data-ttu-id="ade1f-113">Creates the domain level service account that is used by Azure AD Connect to run the sync service.</span><span class="sxs-lookup"><span data-stu-id="ade1f-113">Creates the domain level service account that is used by Azure AD Connect to run the sync service.</span></span>  <span data-ttu-id="ade1f-114">For more information on service accounts, see [Accounts and permissions](active-directory-aadconnect-accounts-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="ade1f-114">For more information on service accounts, see [Accounts and permissions](active-directory-aadconnect-accounts-permissions.md).</span></span>
|<span data-ttu-id="ade1f-115">SQL administrator</span><span class="sxs-lookup"><span data-stu-id="ade1f-115">SQL administrator</span></span>|<span data-ttu-id="ade1f-116">Creates the ADSync database and grants login + dbo access to the Azure AD Connect administrator and the service account created by the domain/forest admin.</span><span class="sxs-lookup"><span data-stu-id="ade1f-116">Creates the ADSync database and grants login + dbo access to the Azure AD Connect administrator and the service account created by the domain/forest admin.</span></span>|
<span data-ttu-id="ade1f-117">Azure AD Connect administrator</span><span class="sxs-lookup"><span data-stu-id="ade1f-117">Azure AD Connect administrator</span></span>|<span data-ttu-id="ade1f-118">Installs Azure AD Connect and specifies the service account during custom installation.</span><span class="sxs-lookup"><span data-stu-id="ade1f-118">Installs Azure AD Connect and specifies the service account during custom installation.</span></span>

## <a name="steps-for-installing-azure-ad-connect-using-sql-delegated-permissions"></a><span data-ttu-id="ade1f-119">Steps for installing Azure AD Connect using SQL delegated permissions</span><span class="sxs-lookup"><span data-stu-id="ade1f-119">Steps for installing Azure AD Connect using SQL delegated permissions</span></span>
<span data-ttu-id="ade1f-120">To provision the database out of band and install Azure AD Connect with database owner permissions, use the following steps.</span><span class="sxs-lookup"><span data-stu-id="ade1f-120">To provision the database out of band and install Azure AD Connect with database owner permissions, use the following steps.</span></span>

>[!NOTE]
><span data-ttu-id="ade1f-121">Although it is not required, it is **highly recommended** that the Latin1_General_CI_AS collation is selected when creating the database.</span><span class="sxs-lookup"><span data-stu-id="ade1f-121">Although it is not required, it is **highly recommended** that the Latin1_General_CI_AS collation is selected when creating the database.</span></span>


1.  <span data-ttu-id="ade1f-122">Have the SQL Administrator create the ADSync database with a case insensitive collation sequence **(Latin1_General_CI_AS)**.</span><span class="sxs-lookup"><span data-stu-id="ade1f-122">Have the SQL Administrator create the ADSync database with a case insensitive collation sequence **(Latin1_General_CI_AS)**.</span></span>  <span data-ttu-id="ade1f-123">The database must be named **ADSync**.</span><span class="sxs-lookup"><span data-stu-id="ade1f-123">The database must be named **ADSync**.</span></span>  <span data-ttu-id="ade1f-124">The recovery model, compatibility level, and containment type are updated to the correct values when Azure AD Connect is installed.</span><span class="sxs-lookup"><span data-stu-id="ade1f-124">The recovery model, compatibility level, and containment type are updated to the correct values when Azure AD Connect is installed.</span></span>  <span data-ttu-id="ade1f-125">However the collation sequence must be set correctly by the SQL administrator otherwise Azure AD Connect will block the installation.</span><span class="sxs-lookup"><span data-stu-id="ade1f-125">However the collation sequence must be set correctly by the SQL administrator otherwise Azure AD Connect will block the installation.</span></span>  <span data-ttu-id="ade1f-126">To recover the SA must delete and recreate the database.</span><span class="sxs-lookup"><span data-stu-id="ade1f-126">To recover the SA must delete and recreate the database.</span></span></br>
<span data-ttu-id="ade1f-127">![Collation](media/active-directory-aadconnect-sql-delegation/sql4.png)</span><span class="sxs-lookup"><span data-stu-id="ade1f-127">![Collation](media/active-directory-aadconnect-sql-delegation/sql4.png)</span></span>
2.  <span data-ttu-id="ade1f-128">Grant the Azure AD Connect administrator and the domain service account the following permissions:</span><span class="sxs-lookup"><span data-stu-id="ade1f-128">Grant the Azure AD Connect administrator and the domain service account the following permissions:</span></span>
    - <span data-ttu-id="ade1f-129">SQL Login</span><span class="sxs-lookup"><span data-stu-id="ade1f-129">SQL Login</span></span> 
    - <span data-ttu-id="ade1f-130">**database owner(dbo)** rights.</span><span class="sxs-lookup"><span data-stu-id="ade1f-130">**database owner(dbo)** rights.</span></span>  </br>
<span data-ttu-id="ade1f-131">![Permissions](media/active-directory-aadconnect-sql-delegation/sql3a.png)</span><span class="sxs-lookup"><span data-stu-id="ade1f-131">![Permissions](media/active-directory-aadconnect-sql-delegation/sql3a.png)</span></span>
3.  <span data-ttu-id="ade1f-132">Send an email to the Azure AD Connect administrator indicating the SQL server and instance name that should be used when installing Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ade1f-132">Send an email to the Azure AD Connect administrator indicating the SQL server and instance name that should be used when installing Azure AD Connect.</span></span>

## <a name="additional-information"></a><span data-ttu-id="ade1f-133">Additional information</span><span class="sxs-lookup"><span data-stu-id="ade1f-133">Additional information</span></span>
<span data-ttu-id="ade1f-134">Once the database is provisioned, the Azure AD Connect administrator can install and configure on-premises synchronization at their convenience.</span><span class="sxs-lookup"><span data-stu-id="ade1f-134">Once the database is provisioned, the Azure AD Connect administrator can install and configure on-premises synchronization at their convenience.</span></span>  

<span data-ttu-id="ade1f-135">The **/UseExistingDatabase** flag is required when using a pre-created database.</span><span class="sxs-lookup"><span data-stu-id="ade1f-135">The **/UseExistingDatabase** flag is required when using a pre-created database.</span></span>  <span data-ttu-id="ade1f-136">It is not only used in recovery situations.</span><span class="sxs-lookup"><span data-stu-id="ade1f-136">It is not only used in recovery situations.</span></span>

<span data-ttu-id="ade1f-137">In addition to supporting new installations of Azure AD Connect, this feature also enables delegation for any scenario related to the **/UseExistingDatabase** flag.</span><span class="sxs-lookup"><span data-stu-id="ade1f-137">In addition to supporting new installations of Azure AD Connect, this feature also enables delegation for any scenario related to the **/UseExistingDatabase** flag.</span></span>  <span data-ttu-id="ade1f-138">For more information on installing Azure AD Connect with an existing database, see [Install Azure AD Connect using an existing ADSync database](active-directory-aadconnect-existing-database.md)</span><span class="sxs-lookup"><span data-stu-id="ade1f-138">For more information on installing Azure AD Connect with an existing database, see [Install Azure AD Connect using an existing ADSync database](active-directory-aadconnect-existing-database.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="ade1f-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="ade1f-139">Next steps</span></span>
- [<span data-ttu-id="ade1f-140">Getting started with Azure AD Connect using express settings</span><span class="sxs-lookup"><span data-stu-id="ade1f-140">Getting started with Azure AD Connect using express settings</span></span>](active-directory-aadconnect-get-started-express.md)
- [<span data-ttu-id="ade1f-141">Custom installation of Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="ade1f-141">Custom installation of Azure AD Connect</span></span>](active-directory-aadconnect-get-started-custom.md)
- [<span data-ttu-id="ade1f-142">Install Azure AD Connect using an existing ADSync database</span><span class="sxs-lookup"><span data-stu-id="ade1f-142">Install Azure AD Connect using an existing ADSync database</span></span>](active-directory-aadconnect-existing-database.md)  
