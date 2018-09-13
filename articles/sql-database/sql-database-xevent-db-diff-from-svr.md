---
title: Extended events in SQL Database | Microsoft Docs
description: Describes extended events (XEvents) in Azure SQL Database, and how event sessions differ slightly from event sessions in Microsoft SQL Server.
services: sql-database
documentationcenter: ''
author: MightyPen
manager: jhubbard
editor: ''
tags: ''
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 8c94c8789696507d89e08a637067ca040d45246a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555351"
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="ab668-103">Extended events in SQL Database</span><span class="sxs-lookup"><span data-stu-id="ab668-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="ab668-104">This topic explains how the implementation of extended events in Azure SQL Database is slightly different compared to extended events in Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ab668-104">This topic explains how the implementation of extended events in Azure SQL Database is slightly different compared to extended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="ab668-105">SQL Database  gained the extended events feature in the second half of calendar 2015.</span><span class="sxs-lookup"><span data-stu-id="ab668-105">SQL Database  gained the extended events feature in the second half of calendar 2015.</span></span>
- <span data-ttu-id="ab668-106">SQL Server has had extended events since 2008.</span><span class="sxs-lookup"><span data-stu-id="ab668-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="ab668-107">The feature set of extended events on SQL Database is a robust subset of the features on SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ab668-107">The feature set of extended events on SQL Database is a robust subset of the features on SQL Server.</span></span>

<span data-ttu-id="ab668-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span><span class="sxs-lookup"><span data-stu-id="ab668-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="ab668-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span><span class="sxs-lookup"><span data-stu-id="ab668-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="ab668-110">Quick Start: Extended events in SQL Server</span><span class="sxs-lookup"><span data-stu-id="ab668-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="ab668-111">Extended Events</span><span class="sxs-lookup"><span data-stu-id="ab668-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="ab668-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ab668-112">Prerequisites</span></span>

<span data-ttu-id="ab668-113">This topic assumes you already have some knowledge of:</span><span class="sxs-lookup"><span data-stu-id="ab668-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="ab668-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="ab668-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="ab668-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ab668-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="ab668-116">The bulk of our documentation about extended events applies to both SQL Server and SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ab668-116">The bulk of our documentation about extended events applies to both SQL Server and SQL Database.</span></span>

<span data-ttu-id="ab668-117">Prior exposure to the following items is helpful when choosing the Event File as the [target](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="ab668-117">Prior exposure to the following items is helpful when choosing the Event File as the [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="ab668-118">Azure Storage service</span><span class="sxs-lookup"><span data-stu-id="ab668-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="ab668-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab668-119">PowerShell</span></span>
    - <span data-ttu-id="ab668-120">[Using Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span><span class="sxs-lookup"><span data-stu-id="ab668-120">[Using Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="ab668-121">Code samples</span><span class="sxs-lookup"><span data-stu-id="ab668-121">Code samples</span></span>

<span data-ttu-id="ab668-122">Related topics provide two code samples:</span><span class="sxs-lookup"><span data-stu-id="ab668-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="ab668-123">Ring Buffer target code for extended events in SQL Database</span><span class="sxs-lookup"><span data-stu-id="ab668-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="ab668-124">Short simple Transact-SQL script.</span><span class="sxs-lookup"><span data-stu-id="ab668-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="ab668-125">We emphasize in the code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span><span class="sxs-lookup"><span data-stu-id="ab668-125">We emphasize in the code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="ab668-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="ab668-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="ab668-127">Event File target code for extended events in SQL Database</span><span class="sxs-lookup"><span data-stu-id="ab668-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="ab668-128">Phase 1 is PowerShell to create an Azure Storage container.</span><span class="sxs-lookup"><span data-stu-id="ab668-128">Phase 1 is PowerShell to create an Azure Storage container.</span></span>
    - <span data-ttu-id="ab668-129">Phase 2 is Transact-SQL that uses the Azure Storage container.</span><span class="sxs-lookup"><span data-stu-id="ab668-129">Phase 2 is Transact-SQL that uses the Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="ab668-130">Transact-SQL differences</span><span class="sxs-lookup"><span data-stu-id="ab668-130">Transact-SQL differences</span></span>


- <span data-ttu-id="ab668-131">When you execute the [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use the **ON SERVER** clause.</span><span class="sxs-lookup"><span data-stu-id="ab668-131">When you execute the [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use the **ON SERVER** clause.</span></span> <span data-ttu-id="ab668-132">But on SQL Database you use the **ON DATABASE** clause instead.</span><span class="sxs-lookup"><span data-stu-id="ab668-132">But on SQL Database you use the **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="ab668-133">The **ON DATABASE** clause also applies to the [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span><span class="sxs-lookup"><span data-stu-id="ab668-133">The **ON DATABASE** clause also applies to the [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="ab668-134">A best practice is to include the event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span><span class="sxs-lookup"><span data-stu-id="ab668-134">A best practice is to include the event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="ab668-135">The **= ON** value supports an automatic restart after a reconfiguration of the logical database due to a failover.</span><span class="sxs-lookup"><span data-stu-id="ab668-135">The **= ON** value supports an automatic restart after a reconfiguration of the logical database due to a failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="ab668-136">New catalog views</span><span class="sxs-lookup"><span data-stu-id="ab668-136">New catalog views</span></span>

<span data-ttu-id="ab668-137">The extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab668-137">The extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="ab668-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in the current database.</span><span class="sxs-lookup"><span data-stu-id="ab668-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in the current database.</span></span> <span data-ttu-id="ab668-139">The views do not return information about instances of active event sessions.</span><span class="sxs-lookup"><span data-stu-id="ab668-139">The views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="ab668-140">Name of</span><span class="sxs-lookup"><span data-stu-id="ab668-140">Name of</span></span><br/><span data-ttu-id="ab668-141">catalog view</span><span class="sxs-lookup"><span data-stu-id="ab668-141">catalog view</span></span> | <span data-ttu-id="ab668-142">Description</span><span class="sxs-lookup"><span data-stu-id="ab668-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ab668-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="ab668-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="ab668-144">Returns a row for each action on each event of an event session.</span><span class="sxs-lookup"><span data-stu-id="ab668-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="ab668-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="ab668-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="ab668-146">Returns a row for each event in an event session.</span><span class="sxs-lookup"><span data-stu-id="ab668-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="ab668-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="ab668-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="ab668-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span><span class="sxs-lookup"><span data-stu-id="ab668-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="ab668-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="ab668-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="ab668-150">Returns a row for each event target for an event session.</span><span class="sxs-lookup"><span data-stu-id="ab668-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="ab668-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="ab668-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="ab668-152">Returns a row for each event session in the SQL Database database.</span><span class="sxs-lookup"><span data-stu-id="ab668-152">Returns a row for each event session in the SQL Database database.</span></span> |

<span data-ttu-id="ab668-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="ab668-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="ab668-154">The name pattern is like **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="ab668-154">The name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="ab668-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="ab668-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="ab668-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span><span class="sxs-lookup"><span data-stu-id="ab668-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="ab668-157">DMVs tell you about *active* event sessions.</span><span class="sxs-lookup"><span data-stu-id="ab668-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="ab668-158">Name of DMV</span><span class="sxs-lookup"><span data-stu-id="ab668-158">Name of DMV</span></span> | <span data-ttu-id="ab668-159">Description</span><span class="sxs-lookup"><span data-stu-id="ab668-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ab668-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="ab668-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="ab668-161">Returns information about event session actions.</span><span class="sxs-lookup"><span data-stu-id="ab668-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="ab668-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="ab668-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="ab668-163">Returns information about session events.</span><span class="sxs-lookup"><span data-stu-id="ab668-163">Returns information about session events.</span></span> |
| <span data-ttu-id="ab668-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="ab668-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="ab668-165">Shows the configuration values for objects that are bound to a session.</span><span class="sxs-lookup"><span data-stu-id="ab668-165">Shows the configuration values for objects that are bound to a session.</span></span> |
| <span data-ttu-id="ab668-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="ab668-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="ab668-167">Returns information about session targets.</span><span class="sxs-lookup"><span data-stu-id="ab668-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="ab668-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="ab668-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="ab668-169">Returns a row for each event session that is scoped to the current database.</span><span class="sxs-lookup"><span data-stu-id="ab668-169">Returns a row for each event session that is scoped to the current database.</span></span> |

<span data-ttu-id="ab668-170">In Microsoft SQL Server, similar catalog views are named without the *\_database* portion of the name, such as:</span><span class="sxs-lookup"><span data-stu-id="ab668-170">In Microsoft SQL Server, similar catalog views are named without the *\_database* portion of the name, such as:</span></span>

- <span data-ttu-id="ab668-171">**sys.dm_xe_sessions**, instead of name</span><span class="sxs-lookup"><span data-stu-id="ab668-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="ab668-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="ab668-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-to-both"></a><span data-ttu-id="ab668-173">DMVs common to both</span><span class="sxs-lookup"><span data-stu-id="ab668-173">DMVs common to both</span></span>
<span data-ttu-id="ab668-174">For extended events there are additional DMVs that are common to both Azure SQL Database and Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="ab668-174">For extended events there are additional DMVs that are common to both Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="ab668-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="ab668-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="ab668-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="ab668-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="ab668-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="ab668-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="ab668-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="ab668-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-the-available-extended-events-actions-and-targets"></a><span data-ttu-id="ab668-179">Find the available extended events, actions, and targets</span><span class="sxs-lookup"><span data-stu-id="ab668-179">Find the available extended events, actions, and targets</span></span>

<span data-ttu-id="ab668-180">You can run a simple SQL **SELECT** to obtain a list of the available events, actions, and target.</span><span class="sxs-lookup"><span data-stu-id="ab668-180">You can run a simple SQL **SELECT** to obtain a list of the available events, actions, and target.</span></span>

```tsql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> <span data-ttu-id="ab668-181">&nbsp;</span><span class="sxs-lookup"><span data-stu-id="ab668-181">&nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="ab668-182">Targets for your SQL Database event sessions</span><span class="sxs-lookup"><span data-stu-id="ab668-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="ab668-183">Here are targets that can capture results from your event sessions on SQL Database:</span><span class="sxs-lookup"><span data-stu-id="ab668-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="ab668-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span><span class="sxs-lookup"><span data-stu-id="ab668-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="ab668-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span><span class="sxs-lookup"><span data-stu-id="ab668-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="ab668-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers to an Azure Storage container.</span><span class="sxs-lookup"><span data-stu-id="ab668-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers to an Azure Storage container.</span></span>

<span data-ttu-id="ab668-187">The [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ab668-187">The [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="ab668-188">Restrictions</span><span class="sxs-lookup"><span data-stu-id="ab668-188">Restrictions</span></span>

<span data-ttu-id="ab668-189">There are a couple of security-related differences befitting the cloud environment of SQL Database:</span><span class="sxs-lookup"><span data-stu-id="ab668-189">There are a couple of security-related differences befitting the cloud environment of SQL Database:</span></span>

- <span data-ttu-id="ab668-190">Extended events are founded on the single-tenant isolation model.</span><span class="sxs-lookup"><span data-stu-id="ab668-190">Extended events are founded on the single-tenant isolation model.</span></span> <span data-ttu-id="ab668-191">An event session in one database cannot access data or events from another database.</span><span class="sxs-lookup"><span data-stu-id="ab668-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="ab668-192">You cannot issue a **CREATE EVENT SESSION** statement in the context of the **master** database.</span><span class="sxs-lookup"><span data-stu-id="ab668-192">You cannot issue a **CREATE EVENT SESSION** statement in the context of the **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="ab668-193">Permission model</span><span class="sxs-lookup"><span data-stu-id="ab668-193">Permission model</span></span>

<span data-ttu-id="ab668-194">You must have **Control** permission on the database to issue a **CREATE EVENT SESSION** statement.</span><span class="sxs-lookup"><span data-stu-id="ab668-194">You must have **Control** permission on the database to issue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="ab668-195">The database owner (dbo) has **Control** permission.</span><span class="sxs-lookup"><span data-stu-id="ab668-195">The database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="ab668-196">Storage container authorizations</span><span class="sxs-lookup"><span data-stu-id="ab668-196">Storage container authorizations</span></span>

<span data-ttu-id="ab668-197">The SAS token you generate for your Azure Storage container must specify **rwl** for the permissions.</span><span class="sxs-lookup"><span data-stu-id="ab668-197">The SAS token you generate for your Azure Storage container must specify **rwl** for the permissions.</span></span> <span data-ttu-id="ab668-198">The **rwl** value provides the following permissions:</span><span class="sxs-lookup"><span data-stu-id="ab668-198">The **rwl** value provides the following permissions:</span></span>

- <span data-ttu-id="ab668-199">Read</span><span class="sxs-lookup"><span data-stu-id="ab668-199">Read</span></span>
- <span data-ttu-id="ab668-200">Write</span><span class="sxs-lookup"><span data-stu-id="ab668-200">Write</span></span>
- <span data-ttu-id="ab668-201">List</span><span class="sxs-lookup"><span data-stu-id="ab668-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="ab668-202">Performance considerations</span><span class="sxs-lookup"><span data-stu-id="ab668-202">Performance considerations</span></span>

<span data-ttu-id="ab668-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for the overall system.</span><span class="sxs-lookup"><span data-stu-id="ab668-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for the overall system.</span></span> <span data-ttu-id="ab668-204">Therefore the Azure SQL Database system dynamically sets and adjusts limits on the amount of active memory that can be accumulated by an event session.</span><span class="sxs-lookup"><span data-stu-id="ab668-204">Therefore the Azure SQL Database system dynamically sets and adjusts limits on the amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="ab668-205">Many factors go into the dynamic calculation.</span><span class="sxs-lookup"><span data-stu-id="ab668-205">Many factors go into the dynamic calculation.</span></span>

<span data-ttu-id="ab668-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span><span class="sxs-lookup"><span data-stu-id="ab668-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="ab668-207">Run fewer concurrent event sessions.</span><span class="sxs-lookup"><span data-stu-id="ab668-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="ab668-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce the amount of memory you specify on the **MAX\_MEMORY** clause.</span><span class="sxs-lookup"><span data-stu-id="ab668-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce the amount of memory you specify on the **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="ab668-209">Network latency</span><span class="sxs-lookup"><span data-stu-id="ab668-209">Network latency</span></span>

<span data-ttu-id="ab668-210">The **Event File** target might experience network latency or failures while persisting data to Azure Storage blobs.</span><span class="sxs-lookup"><span data-stu-id="ab668-210">The **Event File** target might experience network latency or failures while persisting data to Azure Storage blobs.</span></span> <span data-ttu-id="ab668-211">Other events in SQL Database might be delayed while they wait for the network communication to complete.</span><span class="sxs-lookup"><span data-stu-id="ab668-211">Other events in SQL Database might be delayed while they wait for the network communication to complete.</span></span> <span data-ttu-id="ab668-212">This delay can slow your workload.</span><span class="sxs-lookup"><span data-stu-id="ab668-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="ab668-213">To mitigate this performance risk, avoid setting the **EVENT_RETENTION_MODE** option to **NO_EVENT_LOSS** in your event session definitions.</span><span class="sxs-lookup"><span data-stu-id="ab668-213">To mitigate this performance risk, avoid setting the **EVENT_RETENTION_MODE** option to **NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="ab668-214">Related links</span><span class="sxs-lookup"><span data-stu-id="ab668-214">Related links</span></span>

- <span data-ttu-id="ab668-215">[Using Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="ab668-215">[Using Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="ab668-216">Azure Storage Cmdlets</span><span class="sxs-lookup"><span data-stu-id="ab668-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="ab668-217">[Using Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span><span class="sxs-lookup"><span data-stu-id="ab668-217">[Using Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>
- [<span data-ttu-id="ab668-218">How to use Blob storage from .NET</span><span class="sxs-lookup"><span data-stu-id="ab668-218">How to use Blob storage from .NET</span></span>](../storage/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="ab668-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="ab668-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="ab668-220">CREATE EVENT SESSION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="ab668-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="ab668-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="ab668-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="ab668-222">The Azure *Service Updates* webpage, narrowed by parameter to Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="ab668-222">The Azure *Service Updates* webpage, narrowed by parameter to Azure SQL Database:</span></span>
    - [https://azure.microsoft.com/updates/?service=sql-database](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="ab668-223">Other code sample topics for extended events are available at the following links.</span><span class="sxs-lookup"><span data-stu-id="ab668-223">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="ab668-224">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ab668-224">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="ab668-225">Then you can decide whether minor changes are needed to run the sample.</span><span class="sxs-lookup"><span data-stu-id="ab668-225">Then you can decide whether minor changes are needed to run the sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
