

## <a name="create-new-database-user-using-ssms"></a><span data-ttu-id="d7e5e-101">Create new database user using SSMS</span><span class="sxs-lookup"><span data-stu-id="d7e5e-101">Create new database user using SSMS</span></span>
<span data-ttu-id="d7e5e-102">Use the following steps to create a new database user in an existing database using SSMS.</span><span class="sxs-lookup"><span data-stu-id="d7e5e-102">Use the following steps to create a new database user in an existing database using SSMS.</span></span> 

<span data-ttu-id="d7e5e-103">These steps assume that you are connected to SQL Database in Object Explorer using SSMS and are connected to your SQL Database logical server as a server-level principal administrator or with a user account with permissions to create a new user.</span><span class="sxs-lookup"><span data-stu-id="d7e5e-103">These steps assume that you are connected to SQL Database in Object Explorer using SSMS and are connected to your SQL Database logical server as a server-level principal administrator or with a user account with permissions to create a new user.</span></span> 

1. <span data-ttu-id="d7e5e-104">In Object Explorer, expand the Databases node and select the database in which you wish to create a new user account.</span><span class="sxs-lookup"><span data-stu-id="d7e5e-104">In Object Explorer, expand the Databases node and select the database in which you wish to create a new user account.</span></span>
   
     ![SQL Server Management Studio: Connect to SQL Database server](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-create-new-database-user/sql-database-create-new-database-user-1.png)
2. <span data-ttu-id="d7e5e-106">Right-click the selected database and then click **Query**.</span><span class="sxs-lookup"><span data-stu-id="d7e5e-106">Right-click the selected database and then click **Query**.</span></span>
   
     ![SQL Server Management Studio: Connect to SQL Database server](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-create-new-database-user/sql-database-create-new-database-user-2.png)
3. <span data-ttu-id="d7e5e-108">In the query window, edit and use the following Transact-SQL statement to create a contained user in your user database.</span><span class="sxs-lookup"><span data-stu-id="d7e5e-108">In the query window, edit and use the following Transact-SQL statement to create a contained user in your user database.</span></span> 
   
    <span data-ttu-id="d7e5e-109">\`\`\`CREATE USER user1 WITH PASSWORD ='p@ssw0rd1';</span><span class="sxs-lookup"><span data-stu-id="d7e5e-109">\`\`\`CREATE USER user1 WITH PASSWORD ='p@ssw0rd1';</span></span>
    ```
   
     ![SQL Server Management Studio: Connect to SQL Database server](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-create-new-database-user/sql-database-create-new-database-user-3.png)




