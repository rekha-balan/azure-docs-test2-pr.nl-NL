
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-the-connection-string-from-the-azure-portal"></a><span data-ttu-id="b140d-101">Obtain the connection string from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b140d-101">Obtain the connection string from the Azure portal</span></span>
<span data-ttu-id="b140d-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="b140d-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span></span> 

1. <span data-ttu-id="b140d-103">Click **BROWSE** > **SQL databases**.</span><span class="sxs-lookup"><span data-stu-id="b140d-103">Click **BROWSE** > **SQL databases**.</span></span>
2. <span data-ttu-id="b140d-104">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span><span class="sxs-lookup"><span data-stu-id="b140d-104">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span></span>
3. <span data-ttu-id="b140d-105">Click the row for your database.</span><span class="sxs-lookup"><span data-stu-id="b140d-105">Click the row for your database.</span></span>
4. <span data-ttu-id="b140d-106">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span><span class="sxs-lookup"><span data-stu-id="b140d-106">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span></span> 
   
    ![Filter to isolate your database][10-FilterDatabase]
5. <span data-ttu-id="b140d-108">On the blade for your database, click **Show database connection strings**.</span><span class="sxs-lookup"><span data-stu-id="b140d-108">On the blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="b140d-109">If you intend to use the ADO.NET connection library, copy the string labeled **ADO**.</span><span class="sxs-lookup"><span data-stu-id="b140d-109">If you intend to use the ADO.NET connection library, copy the string labeled **ADO**.</span></span> 
   
    ![Copy the ADO connection string for your database][20-CopyAdoConnectionString]
7. <span data-ttu-id="b140d-111">In one format or another, paste the connection string information into your client program code.</span><span class="sxs-lookup"><span data-stu-id="b140d-111">In one format or another, paste the connection string information into your client program code.</span></span>

<span data-ttu-id="b140d-112">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="b140d-112">For more information, see:</span></span><br/><span data-ttu-id="b140d-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span><span class="sxs-lookup"><span data-stu-id="b140d-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[10-FilterDatabase]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->


