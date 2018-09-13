## <a name="invoking-stored-procedure-for-sql-sink"></a><span data-ttu-id="768f6-101">Invoking stored procedure for SQL Sink</span><span class="sxs-lookup"><span data-stu-id="768f6-101">Invoking stored procedure for SQL Sink</span></span>
<span data-ttu-id="768f6-102">When copying data into SQL Server or Azure SQL/SQL Server Database, a user specified stored procedure could be configured and invoked with additional parameters.</span><span class="sxs-lookup"><span data-stu-id="768f6-102">When copying data into SQL Server or Azure SQL/SQL Server Database, a user specified stored procedure could be configured and invoked with additional parameters.</span></span> 

<span data-ttu-id="768f6-103">A stored procedure can be leveraged when built-in copy mechanisms do not serve the purpose.</span><span class="sxs-lookup"><span data-stu-id="768f6-103">A stored procedure can be leveraged when built-in copy mechanisms do not serve the purpose.</span></span> <span data-ttu-id="768f6-104">This is typically leveraged when extra processing (merging columns, looking up additional values, insertion into multiple tables…) needs to be done before the final insertion of source data in the destination table.</span><span class="sxs-lookup"><span data-stu-id="768f6-104">This is typically leveraged when extra processing (merging columns, looking up additional values, insertion into multiple tables…) needs to be done before the final insertion of source data in the destination table.</span></span> 

<span data-ttu-id="768f6-105">You may invoke a stored procedure of choice.</span><span class="sxs-lookup"><span data-stu-id="768f6-105">You may invoke a stored procedure of choice.</span></span> <span data-ttu-id="768f6-106">The following sample shows how to use a stored procedure to do a simple insertion into a table in the database.</span><span class="sxs-lookup"><span data-stu-id="768f6-106">The following sample shows how to use a stored procedure to do a simple insertion into a table in the database.</span></span> 

<span data-ttu-id="768f6-107">**Output dataset**</span><span class="sxs-lookup"><span data-stu-id="768f6-107">**Output dataset**</span></span>

<span data-ttu-id="768f6-108">In this example, type is set to: SqlServerTable.</span><span class="sxs-lookup"><span data-stu-id="768f6-108">In this example, type is set to: SqlServerTable.</span></span> <span data-ttu-id="768f6-109">Set it to AzureSqlTable to use with an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="768f6-109">Set it to AzureSqlTable to use with an Azure SQL database.</span></span> 

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="768f6-110">Define the SqlSink section in copy activity JSON as follows.</span><span class="sxs-lookup"><span data-stu-id="768f6-110">Define the SqlSink section in copy activity JSON as follows.</span></span> <span data-ttu-id="768f6-111">To call a stored procedure while insert data, both SqlWriterStoredProcedureName and SqlWriterTableType properties are needed.</span><span class="sxs-lookup"><span data-stu-id="768f6-111">To call a stored procedure while insert data, both SqlWriterStoredProcedureName and SqlWriterTableType properties are needed.</span></span>

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

<span data-ttu-id="768f6-112">In your database, define the stored procedure with the same name as SqlWriterStoredProcedureName.</span><span class="sxs-lookup"><span data-stu-id="768f6-112">In your database, define the stored procedure with the same name as SqlWriterStoredProcedureName.</span></span> <span data-ttu-id="768f6-113">It handles input data from your specified source, and insert into the output table.</span><span class="sxs-lookup"><span data-stu-id="768f6-113">It handles input data from your specified source, and insert into the output table.</span></span> <span data-ttu-id="768f6-114">Notice that the parameter name of the stored procedure should be the same as the tableName defined in Table JSON file.</span><span class="sxs-lookup"><span data-stu-id="768f6-114">Notice that the parameter name of the stored procedure should be the same as the tableName defined in Table JSON file.</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```
<span data-ttu-id="768f6-115">In your database, define the table type with the same name as SqlWriterTableType.</span><span class="sxs-lookup"><span data-stu-id="768f6-115">In your database, define the table type with the same name as SqlWriterTableType.</span></span> <span data-ttu-id="768f6-116">Notice that the schema of the table type should be same as the schema returned by your input data.</span><span class="sxs-lookup"><span data-stu-id="768f6-116">Notice that the schema of the table type should be same as the schema returned by your input data.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```
<span data-ttu-id="768f6-117">The stored procedure feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="768f6-117">The stored procedure feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span>

