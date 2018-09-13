

## <a name="grant-new-database-user-dbowner-permissions"></a><span data-ttu-id="123d9-101">Grant new database user db_owner permissions</span><span class="sxs-lookup"><span data-stu-id="123d9-101">Grant new database user db_owner permissions</span></span>
<span data-ttu-id="123d9-102">Use the following steps to grant an existing database user db_owner permissions</span><span class="sxs-lookup"><span data-stu-id="123d9-102">Use the following steps to grant an existing database user db_owner permissions</span></span>

<span data-ttu-id="123d9-103">Theses steps assume that you are connected to SQL Database in Object Explorer in SSMS and are connected to your SQL Database logical server as a server-level principal administrator or with a user account with permissions to grant user permissions.</span><span class="sxs-lookup"><span data-stu-id="123d9-103">Theses steps assume that you are connected to SQL Database in Object Explorer in SSMS and are connected to your SQL Database logical server as a server-level principal administrator or with a user account with permissions to grant user permissions.</span></span> 

1. <span data-ttu-id="123d9-104">In Object Explorer, expand the Databases node and select the database with the user to which you wish to grant dbo permissions.</span><span class="sxs-lookup"><span data-stu-id="123d9-104">In Object Explorer, expand the Databases node and select the database with the user to which you wish to grant dbo permissions.</span></span>
   
     ![SQL Server Management Studio: Connect to SQL Database server](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-create-new-database-user/sql-database-create-new-database-user-1.png)
2. <span data-ttu-id="123d9-106">Right-click the selected database and then click **Query**.</span><span class="sxs-lookup"><span data-stu-id="123d9-106">Right-click the selected database and then click **Query**.</span></span>
   
     ![SQL Server Management Studio: Connect to SQL Database server](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-create-new-database-user/sql-database-create-new-database-user-2.png)
3. <span data-ttu-id="123d9-108">In the query window, edit and use the following Transact-SQL statement to grant dbo permissions to a specified user.</span><span class="sxs-lookup"><span data-stu-id="123d9-108">In the query window, edit and use the following Transact-SQL statement to grant dbo permissions to a specified user.</span></span> 
   
    <span data-ttu-id="123d9-109">\`\`\`ALTER ROLE db_owner ADD MEMBER user1;</span><span class="sxs-lookup"><span data-stu-id="123d9-109">\`\`\`ALTER ROLE db_owner ADD MEMBER user1;</span></span>
    ```
   
     ![SQL Server Management Studio: Connect to SQL Database server](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-grant-database-user-dbo-permissions/sql-database-grant-database-user-dbo-permissions-1.png)




