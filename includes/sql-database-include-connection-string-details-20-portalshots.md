<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-the-connection-string-from-the-azure-portal"></a><span data-ttu-id="e9df3-101">Obtain the connection string from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e9df3-101">Obtain the connection string from the Azure portal</span></span>
<span data-ttu-id="e9df3-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="e9df3-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span></span>

1. <span data-ttu-id="e9df3-103">Click **BROWSE** > **SQL databases**.</span><span class="sxs-lookup"><span data-stu-id="e9df3-103">Click **BROWSE** > **SQL databases**.</span></span>
   
    ![Select SQL][1-select-sql]
2. <span data-ttu-id="e9df3-105">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span><span class="sxs-lookup"><span data-stu-id="e9df3-105">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span></span>
   
    ![Select Database][2-select-database]
3. <span data-ttu-id="e9df3-107">Click the row for your database.</span><span class="sxs-lookup"><span data-stu-id="e9df3-107">Click the row for your database.</span></span>
4. <span data-ttu-id="e9df3-108">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span><span class="sxs-lookup"><span data-stu-id="e9df3-108">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span></span>
5. <span data-ttu-id="e9df3-109">Make note of the **SQL database** name and the **Server name**.</span><span class="sxs-lookup"><span data-stu-id="e9df3-109">Make note of the **SQL database** name and the **Server name**.</span></span>  <span data-ttu-id="e9df3-110">The username will be yourusername@yourserver.</span><span class="sxs-lookup"><span data-stu-id="e9df3-110">The username will be yourusername@yourserver.</span></span>
   
    ![Get Connection Details][3-get-connection-details]
6. <span data-ttu-id="e9df3-112">Paste the connection details into your client program code.</span><span class="sxs-lookup"><span data-stu-id="e9df3-112">Paste the connection details into your client program code.</span></span>  <span data-ttu-id="e9df3-113">You will need to replace the {your_password_here} with your real password.</span><span class="sxs-lookup"><span data-stu-id="e9df3-113">You will need to replace the {your_password_here} with your real password.</span></span>

<!--
Could not find a good link for PHP

For more information, see:<br/>[Connection Strings and Configuration Files](https://msdn.microsoft.com/library/ms378428.aspx).
-->


<!-- Image references. -->

[1-select-sql]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-include-connection-string-20-portalshots/connection-string-select-sql.png

[2-select-database]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-include-connection-string-20-portalshots/connection-string-select-database.PNG

[3-get-connection-details]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-include-connection-string-20-portalshots/connection-string-details.PNG


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->



