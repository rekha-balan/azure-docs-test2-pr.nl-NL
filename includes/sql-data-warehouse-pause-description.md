
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, the following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="6d82b-101">To save costs, you can pause and resume compute resources on-demand.</span><span class="sxs-lookup"><span data-stu-id="6d82b-101">To save costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="6d82b-102">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span><span class="sxs-lookup"><span data-stu-id="6d82b-102">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span></span> <span data-ttu-id="6d82b-103">You won't be charged for DWUs while the database is paused.</span><span class="sxs-lookup"><span data-stu-id="6d82b-103">You won't be charged for DWUs while the database is paused.</span></span>

<span data-ttu-id="6d82b-104">When you pause a database:</span><span class="sxs-lookup"><span data-stu-id="6d82b-104">When you pause a database:</span></span>

* <span data-ttu-id="6d82b-105">Compute and memory resources are returned to the pool of available resources in the data center</span><span class="sxs-lookup"><span data-stu-id="6d82b-105">Compute and memory resources are returned to the pool of available resources in the data center</span></span>
* <span data-ttu-id="6d82b-106">DWU costs are zero for the duration of the pause.</span><span class="sxs-lookup"><span data-stu-id="6d82b-106">DWU costs are zero for the duration of the pause.</span></span>
* <span data-ttu-id="6d82b-107">Data storage is not affected and your data stays intact.</span><span class="sxs-lookup"><span data-stu-id="6d82b-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="6d82b-108">SQL Data Warehouse cancels all running or queued operations.</span><span class="sxs-lookup"><span data-stu-id="6d82b-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

