## <a name="specifying-compression"></a><span data-ttu-id="d8d2f-101">Specifying compression</span><span class="sxs-lookup"><span data-stu-id="d8d2f-101">Specifying compression</span></span>
<span data-ttu-id="d8d2f-102">Processing large data sets can cause I/O and network bottlenecks.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-102">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="d8d2f-103">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-103">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="d8d2f-104">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-104">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

> [!NOTE]
> <span data-ttu-id="d8d2f-105">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-105">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="d8d2f-106">When reading files in these format, Data Factory detect and use the compression codec in the metadata; when writing to files in these formats, Data Factory chooses the default compression codec for that format.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-106">When reading files in these format, Data Factory detect and use the compression codec in the metadata; when writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="d8d2f-107">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-107">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>
>
>

<span data-ttu-id="d8d2f-108">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span><span class="sxs-lookup"><span data-stu-id="d8d2f-108">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```
<span data-ttu-id="d8d2f-109">Suppose the above sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-109">Suppose the above sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span></span>   

<span data-ttu-id="d8d2f-110">The **compression** section has two properties:</span><span class="sxs-lookup"><span data-stu-id="d8d2f-110">The **compression** section has two properties:</span></span>  

* <span data-ttu-id="d8d2f-111">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2** or **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-111">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2** or **ZipDeflate**.</span></span>  
* <span data-ttu-id="d8d2f-112">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-112">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="d8d2f-113">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-113">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="d8d2f-114">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-114">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="d8d2f-115">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-115">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="d8d2f-116">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-116">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span></span> <span data-ttu-id="d8d2f-117">Here are a few sample scenarios:</span><span class="sxs-lookup"><span data-stu-id="d8d2f-117">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="d8d2f-118">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-118">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="d8d2f-119">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-119">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="d8d2f-120">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-120">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="d8d2f-121">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-121">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="d8d2f-122">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-122">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="d8d2f-123">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-123">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="d8d2f-124">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-124">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="d8d2f-125">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span><span class="sxs-lookup"><span data-stu-id="d8d2f-125">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span></span>   
