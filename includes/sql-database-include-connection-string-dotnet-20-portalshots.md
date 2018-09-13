<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-the-connection-string-from-the-azure-portal"></a><span data-ttu-id="f4cd2-101">Obtain the connection string from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f4cd2-101">Obtain the connection string from the Azure portal</span></span>
<span data-ttu-id="f4cd2-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="f4cd2-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span></span>

1. <span data-ttu-id="f4cd2-103">Click **BROWSE** > **SQL databases**.</span><span class="sxs-lookup"><span data-stu-id="f4cd2-103">Click **BROWSE** > **SQL databases**.</span></span>
   
    ![Select SQL][1-select-sql]
2. <span data-ttu-id="f4cd2-105">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span><span class="sxs-lookup"><span data-stu-id="f4cd2-105">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span></span>
   
    ![Select Database][2-select-database]
3. <span data-ttu-id="f4cd2-107">Click the row for your database.</span><span class="sxs-lookup"><span data-stu-id="f4cd2-107">Click the row for your database.</span></span>
4. <span data-ttu-id="f4cd2-108">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span><span class="sxs-lookup"><span data-stu-id="f4cd2-108">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span></span>
5. <span data-ttu-id="f4cd2-109">On the blade for your database, click **Show database connection strings**.</span><span class="sxs-lookup"><span data-stu-id="f4cd2-109">On the blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="f4cd2-110">If you intend to use the ADO.NET connection library, copy the string labeled **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="f4cd2-110">If you intend to use the ADO.NET connection library, copy the string labeled **ADO.NET**.</span></span>
   
    ![Copy the ADO.NET connection string for your database][3-get-connection-string]
7. <span data-ttu-id="f4cd2-112">Paste the connection string information into your client program code.</span><span class="sxs-lookup"><span data-stu-id="f4cd2-112">Paste the connection string information into your client program code.</span></span>  <span data-ttu-id="f4cd2-113">You will need to replace the {your_password_here} with your real password.</span><span class="sxs-lookup"><span data-stu-id="f4cd2-113">You will need to replace the {your_password_here} with your real password.</span></span>

<span data-ttu-id="f4cd2-114">For more information, see: [Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4cd2-114">For more information, see: [Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[1-select-sql]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-include-connection-string-20-portalshots/connection-string-select-sql.png


[2-select-database]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-include-connection-string-20-portalshots/connection-string-select-database.PNG

[3-get-connection-string]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-include-connection-string-20-portalshots/connection-string-dotnet.PNG


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->


