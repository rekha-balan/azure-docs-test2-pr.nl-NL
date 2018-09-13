
<!--
includes/sql-database-include-connection-string-30-compare.md

Latest Freshness check:  2015-09-03 , GeneMi.

## Connection string
-->


### <a name="compare-the-connection-string"></a><span data-ttu-id="279d0-101">Compare the connection string</span><span class="sxs-lookup"><span data-stu-id="279d0-101">Compare the connection string</span></span>
<span data-ttu-id="279d0-102">The following table compares the connection strings that your C# program needs to connect to your on-premises SQL Server versus your Azure SQL Database in the cloud.</span><span class="sxs-lookup"><span data-stu-id="279d0-102">The following table compares the connection strings that your C# program needs to connect to your on-premises SQL Server versus your Azure SQL Database in the cloud.</span></span> <span data-ttu-id="279d0-103">The differences are in bold.</span><span class="sxs-lookup"><span data-stu-id="279d0-103">The differences are in bold.</span></span>

| <span data-ttu-id="279d0-104">Connection string for</span><span class="sxs-lookup"><span data-stu-id="279d0-104">Connection string for</span></span><br/><span data-ttu-id="279d0-105">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="279d0-105">Azure SQL Database</span></span> | <span data-ttu-id="279d0-106">Connection string for</span><span class="sxs-lookup"><span data-stu-id="279d0-106">Connection string for</span></span><br/><span data-ttu-id="279d0-107">Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="279d0-107">Microsoft SQL Server</span></span> |
|:--- |:--- |
| <span data-ttu-id="279d0-108">Server=**tcp:**{your_serverName_here}**.database.windows.net,1433**;</span><span class="sxs-lookup"><span data-stu-id="279d0-108">Server=**tcp:**{your_serverName_here}**.database.windows.net,1433**;</span></span><br/><span data-ttu-id="279d0-109">User ID={your_loginName_here}**@{your_serverName_here}**;</span><span class="sxs-lookup"><span data-stu-id="279d0-109">User ID={your_loginName_here}**@{your_serverName_here}**;</span></span><br/><span data-ttu-id="279d0-110">Password={your_password_here};</span><span class="sxs-lookup"><span data-stu-id="279d0-110">Password={your_password_here};</span></span><br/><span data-ttu-id="279d0-111">**Database={your_databaseName_here};**</span><span class="sxs-lookup"><span data-stu-id="279d0-111">**Database={your_databaseName_here};**</span></span><br/><span data-ttu-id="279d0-112">**Connection Timeout=30**;</span><span class="sxs-lookup"><span data-stu-id="279d0-112">**Connection Timeout=30**;</span></span><br/><span data-ttu-id="279d0-113">**Encrypt=True**;</span><span class="sxs-lookup"><span data-stu-id="279d0-113">**Encrypt=True**;</span></span><br/><span data-ttu-id="279d0-114">**TrustServerCertificate=False**;</span><span class="sxs-lookup"><span data-stu-id="279d0-114">**TrustServerCertificate=False**;</span></span> |<span data-ttu-id="279d0-115">Server={your_serverName_here};</span><span class="sxs-lookup"><span data-stu-id="279d0-115">Server={your_serverName_here};</span></span><br/><span data-ttu-id="279d0-116">User ID={your_loginName_here};</span><span class="sxs-lookup"><span data-stu-id="279d0-116">User ID={your_loginName_here};</span></span><br/><span data-ttu-id="279d0-117">Password={your_password_here};</span><span class="sxs-lookup"><span data-stu-id="279d0-117">Password={your_password_here};</span></span> |

<span data-ttu-id="279d0-118">The **Database=** is optional for SQL Server, but is required for SQL Database.</span><span class="sxs-lookup"><span data-stu-id="279d0-118">The **Database=** is optional for SQL Server, but is required for SQL Database.</span></span>

<span data-ttu-id="279d0-119">[.NET ADO SqlConnectionStringBuilder Properties](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder_properties.aspx) - discusses all the parameters in detail.</span><span class="sxs-lookup"><span data-stu-id="279d0-119">[.NET ADO SqlConnectionStringBuilder Properties](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder_properties.aspx) - discusses all the parameters in detail.</span></span>

<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
