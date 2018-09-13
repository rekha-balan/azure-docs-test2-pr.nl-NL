---
title: Connector Version Release History | Microsoft Docs
description: This topic lists all releases of the Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM)
services: active-directory
documentationcenter: ''
author: AndKjell
manager: femila
editor: ''
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/28/2017
ms.author: billmath
ms.openlocfilehash: 244ca634cfd47ee37e3845380ac05dc68d406621
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669255"
---
# <a name="connector-version-release-history"></a><span data-ttu-id="b9366-103">Connector Version Release History</span><span class="sxs-lookup"><span data-stu-id="b9366-103">Connector Version Release History</span></span>
<span data-ttu-id="b9366-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span><span class="sxs-lookup"><span data-stu-id="b9366-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="b9366-105">This topic is on FIM and MIM only.</span><span class="sxs-lookup"><span data-stu-id="b9366-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="b9366-106">These Connectors are not supported on Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b9366-106">These Connectors are not supported on Azure AD Connect.</span></span>

<span data-ttu-id="b9366-107">This topic list all versions of the Connectors that have been released.</span><span class="sxs-lookup"><span data-stu-id="b9366-107">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="b9366-108">Related links:</span><span class="sxs-lookup"><span data-stu-id="b9366-108">Related links:</span></span>

* [<span data-ttu-id="b9366-109">Download Latest Connectors</span><span class="sxs-lookup"><span data-stu-id="b9366-109">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="b9366-110">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span><span class="sxs-lookup"><span data-stu-id="b9366-110">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="b9366-111">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span><span class="sxs-lookup"><span data-stu-id="b9366-111">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="b9366-112">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span><span class="sxs-lookup"><span data-stu-id="b9366-112">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="b9366-113">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span><span class="sxs-lookup"><span data-stu-id="b9366-113">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="b9366-114">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span><span class="sxs-lookup"><span data-stu-id="b9366-114">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>

## <a name="114430"></a><span data-ttu-id="b9366-115">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="b9366-115">1.1.443.0</span></span>

<span data-ttu-id="b9366-116">Released: 2017 March</span><span class="sxs-lookup"><span data-stu-id="b9366-116">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="b9366-117">Enhancements</span><span class="sxs-lookup"><span data-stu-id="b9366-117">Enhancements</span></span>
* <span data-ttu-id="b9366-118">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="b9366-118">Generic SQL:</span></span></br>
  <span data-ttu-id="b9366-119">**Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span><span class="sxs-lookup"><span data-stu-id="b9366-119">**Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br>
  <span data-ttu-id="b9366-120">**Solution description:** In the processing step for references where "\*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span><span class="sxs-lookup"><span data-stu-id="b9366-120">**Solution description:** In the processing step for references where "\*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="b9366-121">This will create many placeholders</span><span class="sxs-lookup"><span data-stu-id="b9366-121">This will create many placeholders</span></span>
- <span data-ttu-id="b9366-122">It is required to make sure the naming is unique cross object types.</span><span class="sxs-lookup"><span data-stu-id="b9366-122">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="b9366-123">Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="b9366-123">Generic LDAP:</span></span></br>
 <span data-ttu-id="b9366-124">**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span><span class="sxs-lookup"><span data-stu-id="b9366-124">**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="b9366-125">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span><span class="sxs-lookup"><span data-stu-id="b9366-125">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="b9366-126">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span><span class="sxs-lookup"><span data-stu-id="b9366-126">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="b9366-127">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="b9366-127">Lotus Domino:</span></span>

  <span data-ttu-id="b9366-128">**Scenario:** Domino mail deletion support for a person removal during an export.</span><span class="sxs-lookup"><span data-stu-id="b9366-128">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br>
  <span data-ttu-id="b9366-129">**Solution:** Configurable mail deletion support for a person removal during an export.</span><span class="sxs-lookup"><span data-stu-id="b9366-129">**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="b9366-130">Fixed issues:</span><span class="sxs-lookup"><span data-stu-id="b9366-130">Fixed issues:</span></span>
* <span data-ttu-id="b9366-131">Generic Web Services:</span><span class="sxs-lookup"><span data-stu-id="b9366-131">Generic Web Services:</span></span>
 * <span data-ttu-id="b9366-132">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span><span class="sxs-lookup"><span data-stu-id="b9366-132">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="b9366-133">Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="b9366-133">Generic LDAP:</span></span>
 * <span data-ttu-id="b9366-134">GLDAP Connector does not see all attributes in AD LDS</span><span class="sxs-lookup"><span data-stu-id="b9366-134">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="b9366-135">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span><span class="sxs-lookup"><span data-stu-id="b9366-135">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="b9366-136">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span><span class="sxs-lookup"><span data-stu-id="b9366-136">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="b9366-137">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span><span class="sxs-lookup"><span data-stu-id="b9366-137">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="b9366-138">LDAP MA.</span><span class="sxs-lookup"><span data-stu-id="b9366-138">LDAP MA.</span></span> <span data-ttu-id="b9366-139">They showed only objects from RootDSE partition.</span><span class="sxs-lookup"><span data-stu-id="b9366-139">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="b9366-140">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="b9366-140">Generic SQL:</span></span>
 * <span data-ttu-id="b9366-141">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span><span class="sxs-lookup"><span data-stu-id="b9366-141">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="b9366-142">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span><span class="sxs-lookup"><span data-stu-id="b9366-142">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="b9366-143">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="b9366-143">Lotus Notes:</span></span>
 * <span data-ttu-id="b9366-144">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span><span class="sxs-lookup"><span data-stu-id="b9366-144">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="b9366-145">Fix for duplicate Certifier error</span><span class="sxs-lookup"><span data-stu-id="b9366-145">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="b9366-146">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span><span class="sxs-lookup"><span data-stu-id="b9366-146">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="b9366-147">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span><span class="sxs-lookup"><span data-stu-id="b9366-147">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="b9366-148">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="b9366-148">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="b9366-149">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span><span class="sxs-lookup"><span data-stu-id="b9366-149">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="b9366-150">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span><span class="sxs-lookup"><span data-stu-id="b9366-150">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="b9366-151">Delete membership not working for cross NAB member.</span><span class="sxs-lookup"><span data-stu-id="b9366-151">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="b9366-152">Values should be successfully deleted from multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="b9366-152">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="b9366-153">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="b9366-153">1.1.117.0</span></span>
<span data-ttu-id="b9366-154">Released: 2016 March</span><span class="sxs-lookup"><span data-stu-id="b9366-154">Released: 2016 March</span></span>

<span data-ttu-id="b9366-155">**New Connector**</span><span class="sxs-lookup"><span data-stu-id="b9366-155">**New Connector**</span></span>  
<span data-ttu-id="b9366-156">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="b9366-156">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="b9366-157">**New features:**</span><span class="sxs-lookup"><span data-stu-id="b9366-157">**New features:**</span></span>

* <span data-ttu-id="b9366-158">Generic LDAP Connector:</span><span class="sxs-lookup"><span data-stu-id="b9366-158">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="b9366-159">Added support for delta import with Isode.</span><span class="sxs-lookup"><span data-stu-id="b9366-159">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="b9366-160">Web Services Connector:</span><span class="sxs-lookup"><span data-stu-id="b9366-160">Web Services Connector:</span></span>
  * <span data-ttu-id="b9366-161">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span><span class="sxs-lookup"><span data-stu-id="b9366-161">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="b9366-162">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span><span class="sxs-lookup"><span data-stu-id="b9366-162">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="b9366-163">Lotus Domino Connector:</span><span class="sxs-lookup"><span data-stu-id="b9366-163">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="b9366-164">For export, you need one certifier per address book.</span><span class="sxs-lookup"><span data-stu-id="b9366-164">For export, you need one certifier per address book.</span></span> <span data-ttu-id="b9366-165">You can now use the same password for all certifiers to make the management easier.</span><span class="sxs-lookup"><span data-stu-id="b9366-165">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="b9366-166">**Fixed issues:**</span><span class="sxs-lookup"><span data-stu-id="b9366-166">**Fixed issues:**</span></span>

* <span data-ttu-id="b9366-167">Generic LDAP Connector:</span><span class="sxs-lookup"><span data-stu-id="b9366-167">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="b9366-168">For IBM Tivoli DS, some reference attributes were not detected correctly.</span><span class="sxs-lookup"><span data-stu-id="b9366-168">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="b9366-169">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span><span class="sxs-lookup"><span data-stu-id="b9366-169">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="b9366-170">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span><span class="sxs-lookup"><span data-stu-id="b9366-170">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="b9366-171">Web Services Connector:</span><span class="sxs-lookup"><span data-stu-id="b9366-171">Web Services Connector:</span></span>
  * <span data-ttu-id="b9366-172">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span><span class="sxs-lookup"><span data-stu-id="b9366-172">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="b9366-173">Lotus Domino Connector:</span><span class="sxs-lookup"><span data-stu-id="b9366-173">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="b9366-174">An export of the fullName attribute to a mail-in database did not work.</span><span class="sxs-lookup"><span data-stu-id="b9366-174">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="b9366-175">An export which both added and removed member from a group only exported the added members.</span><span class="sxs-lookup"><span data-stu-id="b9366-175">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="b9366-176">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span><span class="sxs-lookup"><span data-stu-id="b9366-176">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="b9366-177">Older releases</span><span class="sxs-lookup"><span data-stu-id="b9366-177">Older releases</span></span>
<span data-ttu-id="b9366-178">Before March 2016, the Connectors were released as support topics.</span><span class="sxs-lookup"><span data-stu-id="b9366-178">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="b9366-179">**Generic LDAP**</span><span class="sxs-lookup"><span data-stu-id="b9366-179">**Generic LDAP**</span></span>

* <span data-ttu-id="b9366-180">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span><span class="sxs-lookup"><span data-stu-id="b9366-180">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="b9366-181">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span><span class="sxs-lookup"><span data-stu-id="b9366-181">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="b9366-182">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span><span class="sxs-lookup"><span data-stu-id="b9366-182">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="b9366-183">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span><span class="sxs-lookup"><span data-stu-id="b9366-183">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="b9366-184">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span><span class="sxs-lookup"><span data-stu-id="b9366-184">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="b9366-185">**WebServices**</span><span class="sxs-lookup"><span data-stu-id="b9366-185">**WebServices**</span></span>

* <span data-ttu-id="b9366-186">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span><span class="sxs-lookup"><span data-stu-id="b9366-186">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="b9366-187">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b9366-187">**PowerShell**</span></span>

* <span data-ttu-id="b9366-188">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span><span class="sxs-lookup"><span data-stu-id="b9366-188">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="b9366-189">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="b9366-189">**Lotus Domino**</span></span>

* <span data-ttu-id="b9366-190">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span><span class="sxs-lookup"><span data-stu-id="b9366-190">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="b9366-191">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span><span class="sxs-lookup"><span data-stu-id="b9366-191">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="b9366-192">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span><span class="sxs-lookup"><span data-stu-id="b9366-192">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="b9366-193">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span><span class="sxs-lookup"><span data-stu-id="b9366-193">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="b9366-194">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span><span class="sxs-lookup"><span data-stu-id="b9366-194">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="b9366-195">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span><span class="sxs-lookup"><span data-stu-id="b9366-195">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9366-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="b9366-196">Next steps</span></span>
<span data-ttu-id="b9366-197">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span><span class="sxs-lookup"><span data-stu-id="b9366-197">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="b9366-198">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="b9366-198">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
