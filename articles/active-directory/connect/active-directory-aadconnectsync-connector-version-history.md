---
title: Connector Version Release History | Microsoft Docs
description: This topic lists all releases of the Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM)
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: ''
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/22/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 9bbf75f258f9853803ca4c00155eb186ceca54a3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803293"
---
# <a name="connector-version-release-history"></a><span data-ttu-id="0f540-103">Connector Version Release History</span><span class="sxs-lookup"><span data-stu-id="0f540-103">Connector Version Release History</span></span>
<span data-ttu-id="0f540-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span><span class="sxs-lookup"><span data-stu-id="0f540-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="0f540-105">This topic is on FIM and MIM only.</span><span class="sxs-lookup"><span data-stu-id="0f540-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="0f540-106">These Connectors are not supported for install on Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0f540-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="0f540-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span><span class="sxs-lookup"><span data-stu-id="0f540-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span></span>


<span data-ttu-id="0f540-108">This topic list all versions of the Connectors that have been released.</span><span class="sxs-lookup"><span data-stu-id="0f540-108">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="0f540-109">Related links:</span><span class="sxs-lookup"><span data-stu-id="0f540-109">Related links:</span></span>

* [<span data-ttu-id="0f540-110">Download Latest Connectors</span><span class="sxs-lookup"><span data-stu-id="0f540-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="0f540-111">[Generic LDAP Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericldap) reference documentation</span><span class="sxs-lookup"><span data-stu-id="0f540-111">[Generic LDAP Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericldap) reference documentation</span></span>
* <span data-ttu-id="0f540-112">[Generic SQL Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericsql) reference documentation</span><span class="sxs-lookup"><span data-stu-id="0f540-112">[Generic SQL Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericsql) reference documentation</span></span>
* <span data-ttu-id="0f540-113">[Web Services Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-ma-ws) reference documentation</span><span class="sxs-lookup"><span data-stu-id="0f540-113">[Web Services Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-ma-ws) reference documentation</span></span>
* <span data-ttu-id="0f540-114">[PowerShell Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-powershell) reference documentation</span><span class="sxs-lookup"><span data-stu-id="0f540-114">[PowerShell Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-powershell) reference documentation</span></span>
* <span data-ttu-id="0f540-115">[Lotus Domino Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-domino) reference documentation</span><span class="sxs-lookup"><span data-stu-id="0f540-115">[Lotus Domino Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-domino) reference documentation</span></span>


## <a name="118300"></a><span data-ttu-id="0f540-116">1.1.830.0</span><span class="sxs-lookup"><span data-stu-id="0f540-116">1.1.830.0</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="0f540-117">Fixed issues:</span><span class="sxs-lookup"><span data-stu-id="0f540-117">Fixed issues:</span></span>
* <span data-ttu-id="0f540-118">Resolved ConnectorsLog System.Diagnostics.EventLogInternal.InternalWriteEvent(Message: A device attached to the system is not functioning)</span><span class="sxs-lookup"><span data-stu-id="0f540-118">Resolved ConnectorsLog System.Diagnostics.EventLogInternal.InternalWriteEvent(Message: A device attached to the system is not functioning)</span></span>
* <span data-ttu-id="0f540-119">In this release of connectors you will need to update binding redirect from 3.3.0.0-4.1.3.0 to 4.1.4.0 in miiserver.exe.config</span><span class="sxs-lookup"><span data-stu-id="0f540-119">In this release of connectors you will need to update binding redirect from 3.3.0.0-4.1.3.0 to 4.1.4.0 in miiserver.exe.config</span></span>
* <span data-ttu-id="0f540-120">Generic Web Services:</span><span class="sxs-lookup"><span data-stu-id="0f540-120">Generic Web Services:</span></span>
    * <span data-ttu-id="0f540-121">Resolved Valid JSON response could not be saved in configuration tool</span><span class="sxs-lookup"><span data-stu-id="0f540-121">Resolved Valid JSON response could not be saved in configuration tool</span></span>
* <span data-ttu-id="0f540-122">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="0f540-122">Generic SQL:</span></span>
    * <span data-ttu-id="0f540-123">Export always generates only update query for the operation of deleting.</span><span class="sxs-lookup"><span data-stu-id="0f540-123">Export always generates only update query for the operation of deleting.</span></span> <span data-ttu-id="0f540-124">Added to generate a delete query</span><span class="sxs-lookup"><span data-stu-id="0f540-124">Added to generate a delete query</span></span>
    * <span data-ttu-id="0f540-125">The SQL query which gets objects for the operation of Delta Import,  if ‘Delta Strategy’ is ‘Change Tracking’ was fixed.</span><span class="sxs-lookup"><span data-stu-id="0f540-125">The SQL query which gets objects for the operation of Delta Import,  if ‘Delta Strategy’ is ‘Change Tracking’ was fixed.</span></span> <span data-ttu-id="0f540-126">In this implementation known limitation:  Delta Import with ‘Change Tracking’ mode does not track changes in multi-valued attributes</span><span class="sxs-lookup"><span data-stu-id="0f540-126">In this implementation known limitation:  Delta Import with ‘Change Tracking’ mode does not track changes in multi-valued attributes</span></span>
    * <span data-ttu-id="0f540-127">Added possibility to generate a delete query for case, when it is necessary to delete the last value of multivalued attribute and this row does not contain any other data except value which it is necessary to delete.</span><span class="sxs-lookup"><span data-stu-id="0f540-127">Added possibility to generate a delete query for case, when it is necessary to delete the last value of multivalued attribute and this row does not contain any other data except value which it is necessary to delete.</span></span>
    * <span data-ttu-id="0f540-128">System.ArgumentException handling when implemented OUTPUT parameters by SP</span><span class="sxs-lookup"><span data-stu-id="0f540-128">System.ArgumentException handling when implemented OUTPUT parameters by SP</span></span> 
    * <span data-ttu-id="0f540-129">Incorrect query to make the operation of export into field which has varbinary(max) type</span><span class="sxs-lookup"><span data-stu-id="0f540-129">Incorrect query to make the operation of export into field which has varbinary(max) type</span></span>
    * <span data-ttu-id="0f540-130">Issue with parameterList variable was initialized twice (in the functions ExportAttributes and GetQueryForMultiValue)</span><span class="sxs-lookup"><span data-stu-id="0f540-130">Issue with parameterList variable was initialized twice (in the functions ExportAttributes and GetQueryForMultiValue)</span></span>


## <a name="116490-aadconnect-116490"></a><span data-ttu-id="0f540-131">1.1.649.0 (AADConnect 1.1.649.0)</span><span class="sxs-lookup"><span data-stu-id="0f540-131">1.1.649.0 (AADConnect 1.1.649.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="0f540-132">Fixed issues:</span><span class="sxs-lookup"><span data-stu-id="0f540-132">Fixed issues:</span></span>

* <span data-ttu-id="0f540-133">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="0f540-133">Lotus Notes:</span></span>
  * <span data-ttu-id="0f540-134">Filtering custom certifiers option</span><span class="sxs-lookup"><span data-stu-id="0f540-134">Filtering custom certifiers option</span></span>
  * <span data-ttu-id="0f540-135">Import of the class ImportOperations fixed the definition of what operations can be run in the 'Views' mode and which in the 'Search' mode.</span><span class="sxs-lookup"><span data-stu-id="0f540-135">Import of the class ImportOperations fixed the definition of what operations can be run in the 'Views' mode and which in the 'Search' mode.</span></span>
* <span data-ttu-id="0f540-136">Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="0f540-136">Generic LDAP:</span></span>
  * <span data-ttu-id="0f540-137">OpenLDAP Directory uses DN as anchor rather than entryUUI.</span><span class="sxs-lookup"><span data-stu-id="0f540-137">OpenLDAP Directory uses DN as anchor rather than entryUUI.</span></span> <span data-ttu-id="0f540-138">New option to GLDAP connector which allows to modify anchor</span><span class="sxs-lookup"><span data-stu-id="0f540-138">New option to GLDAP connector which allows to modify anchor</span></span>
* <span data-ttu-id="0f540-139">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="0f540-139">Generic SQL:</span></span>
  * <span data-ttu-id="0f540-140">Fixed export into field which has varbinary(max) type.</span><span class="sxs-lookup"><span data-stu-id="0f540-140">Fixed export into field which has varbinary(max) type.</span></span>
  * <span data-ttu-id="0f540-141">When adding binary data from a data source to CSEntry object, The DataTypeConversion function failed on zero bytes.</span><span class="sxs-lookup"><span data-stu-id="0f540-141">When adding binary data from a data source to CSEntry object, The DataTypeConversion function failed on zero bytes.</span></span> <span data-ttu-id="0f540-142">Fixed DataTypeConversion function of the CSEntryOperationBase class.</span><span class="sxs-lookup"><span data-stu-id="0f540-142">Fixed DataTypeConversion function of the CSEntryOperationBase class.</span></span>




### <a name="enhancements"></a><span data-ttu-id="0f540-143">Enhancements:</span><span class="sxs-lookup"><span data-stu-id="0f540-143">Enhancements:</span></span>

* <span data-ttu-id="0f540-144">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="0f540-144">Generic SQL:</span></span>
  * <span data-ttu-id="0f540-145">The ability to configure the mode for execute stored procedure with named parameters or not named is added in a configuration window of the Generic SQL management agent in the page 'Global Parameters'.</span><span class="sxs-lookup"><span data-stu-id="0f540-145">The ability to configure the mode for execute stored procedure with named parameters or not named is added in a configuration window of the Generic SQL management agent in the page 'Global Parameters'.</span></span> <span data-ttu-id="0f540-146">In the page 'Global Parameters' there is check box with the label 'Use named parameters to execute a stored procedure' which is responsible for mode for execute stored procedure with named parameters or not.</span><span class="sxs-lookup"><span data-stu-id="0f540-146">In the page 'Global Parameters' there is check box with the label 'Use named parameters to execute a stored procedure' which is responsible for mode for execute stored procedure with named parameters or not.</span></span>
    * <span data-ttu-id="0f540-147">Currently, the ability to execute stored procedure with named parameters works only for databases IBM DB2 and MSSQL.</span><span class="sxs-lookup"><span data-stu-id="0f540-147">Currently, the ability to execute stored procedure with named parameters works only for databases IBM DB2 and MSSQL.</span></span> <span data-ttu-id="0f540-148">For databases Oracle and MySQL this approach doesn’t work:</span><span class="sxs-lookup"><span data-stu-id="0f540-148">For databases Oracle and MySQL this approach doesn’t work:</span></span> 
      * <span data-ttu-id="0f540-149">The SQL syntaxes of MySQL doesn’t support named parameters in stored procedures.</span><span class="sxs-lookup"><span data-stu-id="0f540-149">The SQL syntaxes of MySQL doesn’t support named parameters in stored procedures.</span></span>
      * <span data-ttu-id="0f540-150">The ODBC driver for the Oracle doesn’t support named parameters for named parameters in stored procedures)</span><span class="sxs-lookup"><span data-stu-id="0f540-150">The ODBC driver for the Oracle doesn’t support named parameters for named parameters in stored procedures)</span></span>

## <a name="116040-aadconnect-116140"></a><span data-ttu-id="0f540-151">1.1.604.0 (AADConnect 1.1.614.0)</span><span class="sxs-lookup"><span data-stu-id="0f540-151">1.1.604.0 (AADConnect 1.1.614.0)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="0f540-152">Fixed issues:</span><span class="sxs-lookup"><span data-stu-id="0f540-152">Fixed issues:</span></span>

* <span data-ttu-id="0f540-153">Generic Web Services:</span><span class="sxs-lookup"><span data-stu-id="0f540-153">Generic Web Services:</span></span>
  * <span data-ttu-id="0f540-154">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span><span class="sxs-lookup"><span data-stu-id="0f540-154">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="0f540-155">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="0f540-155">Generic SQL:</span></span>
  * <span data-ttu-id="0f540-156">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span><span class="sxs-lookup"><span data-stu-id="0f540-156">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span></span> <span data-ttu-id="0f540-157">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span><span class="sxs-lookup"><span data-stu-id="0f540-157">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="0f540-158">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="0f540-158">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="0f540-159">Fixed issues:</span><span class="sxs-lookup"><span data-stu-id="0f540-159">Fixed issues:</span></span>

* <span data-ttu-id="0f540-160">Generic Web Services:</span><span class="sxs-lookup"><span data-stu-id="0f540-160">Generic Web Services:</span></span>
  * <span data-ttu-id="0f540-161">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span><span class="sxs-lookup"><span data-stu-id="0f540-161">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span></span> <span data-ttu-id="0f540-162">This caused problems with serialization this Json array for the REST request.</span><span class="sxs-lookup"><span data-stu-id="0f540-162">This caused problems with serialization this Json array for the REST request.</span></span>
  * <span data-ttu-id="0f540-163">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span><span class="sxs-lookup"><span data-stu-id="0f540-163">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="0f540-164">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="0f540-164">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>
> [!NOTE]
> <span data-ttu-id="0f540-165">JSONSpaceNamePattern key is required as for export you will recieve the following error: Message: Empty name is not legal.</span><span class="sxs-lookup"><span data-stu-id="0f540-165">JSONSpaceNamePattern key is required as for export you will recieve the following error: Message: Empty name is not legal.</span></span> 

* <span data-ttu-id="0f540-166">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="0f540-166">Lotus Notes:</span></span>
  * <span data-ttu-id="0f540-167">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span><span class="sxs-lookup"><span data-stu-id="0f540-167">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span></span> 
    * <span data-ttu-id="0f540-168">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span><span class="sxs-lookup"><span data-stu-id="0f540-168">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span></span>  
      - <span data-ttu-id="0f540-169">LastName</span><span class="sxs-lookup"><span data-stu-id="0f540-169">LastName</span></span>
      - <span data-ttu-id="0f540-170">FirstName</span><span class="sxs-lookup"><span data-stu-id="0f540-170">FirstName</span></span>
      - <span data-ttu-id="0f540-171">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="0f540-171">MiddleInitial</span></span>
      - <span data-ttu-id="0f540-172">AltFullName</span><span class="sxs-lookup"><span data-stu-id="0f540-172">AltFullName</span></span>
      - <span data-ttu-id="0f540-173">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="0f540-173">AltFullNameLanguage</span></span>
      - <span data-ttu-id="0f540-174">ou</span><span class="sxs-lookup"><span data-stu-id="0f540-174">ou</span></span>
      - <span data-ttu-id="0f540-175">altcommonname</span><span class="sxs-lookup"><span data-stu-id="0f540-175">altcommonname</span></span>

  * <span data-ttu-id="0f540-176">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span><span class="sxs-lookup"><span data-stu-id="0f540-176">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="0f540-177">Enhancements:</span><span class="sxs-lookup"><span data-stu-id="0f540-177">Enhancements:</span></span>

* <span data-ttu-id="0f540-178">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="0f540-178">Generic SQL:</span></span>
  * <span data-ttu-id="0f540-179">**Scenario: redesigned Implemented:** "\*" feature</span><span class="sxs-lookup"><span data-stu-id="0f540-179">**Scenario: redesigned Implemented:** "\*" feature</span></span>
  * <span data-ttu-id="0f540-180">**Solution description:** Changed approach for [multi-valued reference attributes handling](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericsql).</span><span class="sxs-lookup"><span data-stu-id="0f540-180">**Solution description:** Changed approach for [multi-valued reference attributes handling](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericsql).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="0f540-181">Fixed issues:</span><span class="sxs-lookup"><span data-stu-id="0f540-181">Fixed issues:</span></span>

* <span data-ttu-id="0f540-182">Generic Web Services:</span><span class="sxs-lookup"><span data-stu-id="0f540-182">Generic Web Services:</span></span>
  * <span data-ttu-id="0f540-183">Can’t import Server configuration if WebService Connector is present</span><span class="sxs-lookup"><span data-stu-id="0f540-183">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="0f540-184">WebService Connector is not working with multiple  Web Services</span><span class="sxs-lookup"><span data-stu-id="0f540-184">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="0f540-185">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="0f540-185">Generic SQL:</span></span>
  * <span data-ttu-id="0f540-186">No object types are listed for single value referenced attribute</span><span class="sxs-lookup"><span data-stu-id="0f540-186">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="0f540-187">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span><span class="sxs-lookup"><span data-stu-id="0f540-187">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="0f540-188">OverflowException in GSQL connector with DB2 on AS/400</span><span class="sxs-lookup"><span data-stu-id="0f540-188">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="0f540-189">Lotus:</span><span class="sxs-lookup"><span data-stu-id="0f540-189">Lotus:</span></span>
  * <span data-ttu-id="0f540-190">Added option to enable\disable searching OUs before opening GlobalParameters page</span><span class="sxs-lookup"><span data-stu-id="0f540-190">Added option to enable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="0f540-191">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="0f540-191">1.1.443.0</span></span>

<span data-ttu-id="0f540-192">Released: 2017 March</span><span class="sxs-lookup"><span data-stu-id="0f540-192">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="0f540-193">Enhancements</span><span class="sxs-lookup"><span data-stu-id="0f540-193">Enhancements</span></span>

* <span data-ttu-id="0f540-194">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="0f540-194">Generic SQL:</span></span></br>
  <span data-ttu-id="0f540-195">**Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span><span class="sxs-lookup"><span data-stu-id="0f540-195">**Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br>
  <span data-ttu-id="0f540-196">**Solution description:** In the processing step for references were "\*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span><span class="sxs-lookup"><span data-stu-id="0f540-196">**Solution description:** In the processing step for references were "\*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="0f540-197">This will create many placeholders</span><span class="sxs-lookup"><span data-stu-id="0f540-197">This will create many placeholders</span></span>
- <span data-ttu-id="0f540-198">It is required to make sure the naming is unique cross object types.</span><span class="sxs-lookup"><span data-stu-id="0f540-198">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="0f540-199">Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="0f540-199">Generic LDAP:</span></span></br>
 <span data-ttu-id="0f540-200">**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span><span class="sxs-lookup"><span data-stu-id="0f540-200">**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="0f540-201">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span><span class="sxs-lookup"><span data-stu-id="0f540-201">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="0f540-202">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span><span class="sxs-lookup"><span data-stu-id="0f540-202">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="0f540-203">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="0f540-203">Lotus Domino:</span></span>

  <span data-ttu-id="0f540-204">**Scenario:** Domino mail deletion support for a person removal during an export.</span><span class="sxs-lookup"><span data-stu-id="0f540-204">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br>
  <span data-ttu-id="0f540-205">**Solution:** Configurable mail deletion support for a person removal during an export.</span><span class="sxs-lookup"><span data-stu-id="0f540-205">**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="0f540-206">Fixed issues:</span><span class="sxs-lookup"><span data-stu-id="0f540-206">Fixed issues:</span></span>
* <span data-ttu-id="0f540-207">Generic Web Services:</span><span class="sxs-lookup"><span data-stu-id="0f540-207">Generic Web Services:</span></span>
 * <span data-ttu-id="0f540-208">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span><span class="sxs-lookup"><span data-stu-id="0f540-208">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="0f540-209">Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="0f540-209">Generic LDAP:</span></span>
 * <span data-ttu-id="0f540-210">GLDAP Connector does not see all attributes in AD LDS</span><span class="sxs-lookup"><span data-stu-id="0f540-210">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="0f540-211">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span><span class="sxs-lookup"><span data-stu-id="0f540-211">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="0f540-212">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span><span class="sxs-lookup"><span data-stu-id="0f540-212">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="0f540-213">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span><span class="sxs-lookup"><span data-stu-id="0f540-213">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="0f540-214">LDAP MA.</span><span class="sxs-lookup"><span data-stu-id="0f540-214">LDAP MA.</span></span> <span data-ttu-id="0f540-215">They showed only objects from RootDSE partition.</span><span class="sxs-lookup"><span data-stu-id="0f540-215">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="0f540-216">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="0f540-216">Generic SQL:</span></span>
 * <span data-ttu-id="0f540-217">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span><span class="sxs-lookup"><span data-stu-id="0f540-217">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="0f540-218">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span><span class="sxs-lookup"><span data-stu-id="0f540-218">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="0f540-219">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="0f540-219">Lotus Notes:</span></span>
 * <span data-ttu-id="0f540-220">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span><span class="sxs-lookup"><span data-stu-id="0f540-220">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="0f540-221">Fix for duplicate Certifier error</span><span class="sxs-lookup"><span data-stu-id="0f540-221">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="0f540-222">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span><span class="sxs-lookup"><span data-stu-id="0f540-222">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="0f540-223">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span><span class="sxs-lookup"><span data-stu-id="0f540-223">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="0f540-224">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="0f540-224">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="0f540-225">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span><span class="sxs-lookup"><span data-stu-id="0f540-225">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="0f540-226">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span><span class="sxs-lookup"><span data-stu-id="0f540-226">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="0f540-227">Delete membership not working for cross NAB member.</span><span class="sxs-lookup"><span data-stu-id="0f540-227">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="0f540-228">Values should be successfully deleted from multi-valued attribute</span><span class="sxs-lookup"><span data-stu-id="0f540-228">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="0f540-229">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="0f540-229">1.1.117.0</span></span>
<span data-ttu-id="0f540-230">Released: 2016 March</span><span class="sxs-lookup"><span data-stu-id="0f540-230">Released: 2016 March</span></span>

<span data-ttu-id="0f540-231">**New Connector**</span><span class="sxs-lookup"><span data-stu-id="0f540-231">**New Connector**</span></span>  
<span data-ttu-id="0f540-232">Initial release of the [Generic SQL Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericsql).</span><span class="sxs-lookup"><span data-stu-id="0f540-232">Initial release of the [Generic SQL Connector](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericsql).</span></span>

<span data-ttu-id="0f540-233">**New features:**</span><span class="sxs-lookup"><span data-stu-id="0f540-233">**New features:**</span></span>

* <span data-ttu-id="0f540-234">Generic LDAP Connector:</span><span class="sxs-lookup"><span data-stu-id="0f540-234">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="0f540-235">Added support for delta import with Isode.</span><span class="sxs-lookup"><span data-stu-id="0f540-235">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="0f540-236">Web Services Connector:</span><span class="sxs-lookup"><span data-stu-id="0f540-236">Web Services Connector:</span></span>
  * <span data-ttu-id="0f540-237">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span><span class="sxs-lookup"><span data-stu-id="0f540-237">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="0f540-238">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span><span class="sxs-lookup"><span data-stu-id="0f540-238">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="0f540-239">Lotus Domino Connector:</span><span class="sxs-lookup"><span data-stu-id="0f540-239">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="0f540-240">For export, you need one certifier per address book.</span><span class="sxs-lookup"><span data-stu-id="0f540-240">For export, you need one certifier per address book.</span></span> <span data-ttu-id="0f540-241">You can now use the same password for all certifiers to make the management easier.</span><span class="sxs-lookup"><span data-stu-id="0f540-241">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="0f540-242">**Fixed issues:**</span><span class="sxs-lookup"><span data-stu-id="0f540-242">**Fixed issues:**</span></span>

* <span data-ttu-id="0f540-243">Generic LDAP Connector:</span><span class="sxs-lookup"><span data-stu-id="0f540-243">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="0f540-244">For IBM Tivoli DS, some reference attributes were not detected correctly.</span><span class="sxs-lookup"><span data-stu-id="0f540-244">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="0f540-245">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span><span class="sxs-lookup"><span data-stu-id="0f540-245">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="0f540-246">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span><span class="sxs-lookup"><span data-stu-id="0f540-246">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="0f540-247">Web Services Connector:</span><span class="sxs-lookup"><span data-stu-id="0f540-247">Web Services Connector:</span></span>
  * <span data-ttu-id="0f540-248">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span><span class="sxs-lookup"><span data-stu-id="0f540-248">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="0f540-249">Lotus Domino Connector:</span><span class="sxs-lookup"><span data-stu-id="0f540-249">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="0f540-250">An export of the fullName attribute to a mail-in database did not work.</span><span class="sxs-lookup"><span data-stu-id="0f540-250">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="0f540-251">An export which both added and removed member from a group only exported the added members.</span><span class="sxs-lookup"><span data-stu-id="0f540-251">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="0f540-252">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span><span class="sxs-lookup"><span data-stu-id="0f540-252">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="0f540-253">Older releases</span><span class="sxs-lookup"><span data-stu-id="0f540-253">Older releases</span></span>
<span data-ttu-id="0f540-254">Before March 2016, the Connectors were released as support topics.</span><span class="sxs-lookup"><span data-stu-id="0f540-254">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="0f540-255">**Generic LDAP**</span><span class="sxs-lookup"><span data-stu-id="0f540-255">**Generic LDAP**</span></span>

* <span data-ttu-id="0f540-256">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span><span class="sxs-lookup"><span data-stu-id="0f540-256">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="0f540-257">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span><span class="sxs-lookup"><span data-stu-id="0f540-257">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="0f540-258">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span><span class="sxs-lookup"><span data-stu-id="0f540-258">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="0f540-259">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span><span class="sxs-lookup"><span data-stu-id="0f540-259">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="0f540-260">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span><span class="sxs-lookup"><span data-stu-id="0f540-260">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="0f540-261">**WebServices**</span><span class="sxs-lookup"><span data-stu-id="0f540-261">**WebServices**</span></span>

* <span data-ttu-id="0f540-262">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span><span class="sxs-lookup"><span data-stu-id="0f540-262">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="0f540-263">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="0f540-263">**PowerShell**</span></span>

* <span data-ttu-id="0f540-264">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span><span class="sxs-lookup"><span data-stu-id="0f540-264">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="0f540-265">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="0f540-265">**Lotus Domino**</span></span>

* <span data-ttu-id="0f540-266">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span><span class="sxs-lookup"><span data-stu-id="0f540-266">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="0f540-267">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span><span class="sxs-lookup"><span data-stu-id="0f540-267">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="0f540-268">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span><span class="sxs-lookup"><span data-stu-id="0f540-268">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="0f540-269">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span><span class="sxs-lookup"><span data-stu-id="0f540-269">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="0f540-270">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span><span class="sxs-lookup"><span data-stu-id="0f540-270">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="0f540-271">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span><span class="sxs-lookup"><span data-stu-id="0f540-271">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0f540-272">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="0f540-272">Troubleshooting</span></span> 

> [!NOTE]
> <span data-ttu-id="0f540-273">When updating Microsoft Identity Manager or AADConnect with use of any of ECMA2 connectors.</span><span class="sxs-lookup"><span data-stu-id="0f540-273">When updating Microsoft Identity Manager or AADConnect with use of any of ECMA2 connectors.</span></span> 

<span data-ttu-id="0f540-274">You must refresh the connector definition upon upgrade to match or you will receive the following error in the application event log start to report warning ID 6947: "Assembly version in AAD Connector configuration ("X.X.XXX.X") is earlier than the actual version ("X.X.XXX.X") of "C:\Program Files\Microsoft Azure AD Sync\Extensions\Microsoft.IAM.Connector.GenericLdap.dll".</span><span class="sxs-lookup"><span data-stu-id="0f540-274">You must refresh the connector definition upon upgrade to match or you will receive the following error in the application event log start to report warning ID 6947: "Assembly version in AAD Connector configuration ("X.X.XXX.X") is earlier than the actual version ("X.X.XXX.X") of "C:\Program Files\Microsoft Azure AD Sync\Extensions\Microsoft.IAM.Connector.GenericLdap.dll".</span></span>

<span data-ttu-id="0f540-275">To refresh the definition:</span><span class="sxs-lookup"><span data-stu-id="0f540-275">To refresh the definition:</span></span>
* <span data-ttu-id="0f540-276">Open the Properties for the Connector instance</span><span class="sxs-lookup"><span data-stu-id="0f540-276">Open the Properties for the Connector instance</span></span>
* <span data-ttu-id="0f540-277">Click the Connection / Connect to tab</span><span class="sxs-lookup"><span data-stu-id="0f540-277">Click the Connection / Connect to tab</span></span>
  * <span data-ttu-id="0f540-278">Enter the password for the Connector account</span><span class="sxs-lookup"><span data-stu-id="0f540-278">Enter the password for the Connector account</span></span>
* <span data-ttu-id="0f540-279">Click each of the property tabs, in turn</span><span class="sxs-lookup"><span data-stu-id="0f540-279">Click each of the property tabs, in turn</span></span>
  * <span data-ttu-id="0f540-280">If this Connector type has a Partitions tab, with a Refresh button, click the Refresh button while on that tab</span><span class="sxs-lookup"><span data-stu-id="0f540-280">If this Connector type has a Partitions tab, with a Refresh button, click the Refresh button while on that tab</span></span>
* <span data-ttu-id="0f540-281">After all property tabs have been accessed, click the OK button to save the changes.</span><span class="sxs-lookup"><span data-stu-id="0f540-281">After all property tabs have been accessed, click the OK button to save the changes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0f540-282">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f540-282">Next steps</span></span>
<span data-ttu-id="0f540-283">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span><span class="sxs-lookup"><span data-stu-id="0f540-283">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="0f540-284">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="0f540-284">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
