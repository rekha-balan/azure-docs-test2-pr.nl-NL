---
title: Use ScaleR and SparkR with Azure HDInsight | Microsoft Docs
description: Use ScaleR and SparkR with R Server and HDInsight
services: hdinsight
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeffstok
ms.openlocfilehash: bab5268c4aab2210e8ace2c3a1db23b34887c2ed
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540968"
---
# <a name="combining-scaler-and-sparkr-in-hdinsight"></a><span data-ttu-id="65872-103">Combining ScaleR and SparkR in HDInsight</span><span class="sxs-lookup"><span data-stu-id="65872-103">Combining ScaleR and SparkR in HDInsight</span></span>

<span data-ttu-id="65872-104">Learn how to combine the capabilities of ScaleR for data manipulation on Spark with Microsoft R Server for analytics.</span><span class="sxs-lookup"><span data-stu-id="65872-104">Learn how to combine the capabilities of ScaleR for data manipulation on Spark with Microsoft R Server for analytics.</span></span> <span data-ttu-id="65872-105">Although both packages run on top of Hadoop’s Spark execution engine to leverage the latest capabilities in distributed processing, they are blocked from in-memory data sharing by requiring their own Spark sessions.</span><span class="sxs-lookup"><span data-stu-id="65872-105">Although both packages run on top of Hadoop’s Spark execution engine to leverage the latest capabilities in distributed processing, they are blocked from in-memory data sharing by requiring their own Spark sessions.</span></span> <span data-ttu-id="65872-106">Until this is addressed in an upcoming version of R Server, the workaround is to maintain non-overlapping Spark sessions, and exchange data through intermediate files.</span><span class="sxs-lookup"><span data-stu-id="65872-106">Until this is addressed in an upcoming version of R Server, the workaround is to maintain non-overlapping Spark sessions, and exchange data through intermediate files.</span></span> <span data-ttu-id="65872-107">As you’ll see, both these requirements are quite straightforward to achieve.</span><span class="sxs-lookup"><span data-stu-id="65872-107">As you’ll see, both these requirements are quite straightforward to achieve.</span></span>

<span data-ttu-id="65872-108">To demonstrate we’ll use an example initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd also available through the webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). The example uses SparkR to join the well-known airlines arrival delay data set with weather data at departure and arrival airports, and use that as input to a ScaleR logistic regression model for predicting flight arrival delay.</span><span class="sxs-lookup"><span data-stu-id="65872-108">To demonstrate we’ll use an example initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd also available through the webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). The example uses SparkR to join the well-known airlines arrival delay data set with weather data at departure and arrival airports, and use that as input to a ScaleR logistic regression model for predicting flight arrival delay.</span></span>

<span data-ttu-id="65872-109">The code we’ll walkthrough was originally written for R Server running on Spark in an HDInsight cluster in Azure, but the concept of mixing use of SparkR and ScaleR in one script applies equally to on-premise environments.</span><span class="sxs-lookup"><span data-stu-id="65872-109">The code we’ll walkthrough was originally written for R Server running on Spark in an HDInsight cluster in Azure, but the concept of mixing use of SparkR and ScaleR in one script applies equally to on-premise environments.</span></span> <span data-ttu-id="65872-110">In the following, we presume an intermediate level of knowledge of R and R Server’s [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library, and introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) along the way.</span><span class="sxs-lookup"><span data-stu-id="65872-110">In the following, we presume an intermediate level of knowledge of R and R Server’s [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library, and introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) along the way.</span></span>

## <a name="the-airline-and-weather-datasets"></a><span data-ttu-id="65872-111">The airline and weather datasets</span><span class="sxs-lookup"><span data-stu-id="65872-111">The airline and weather datasets</span></span>

<span data-ttu-id="65872-112">The AirOnTime08to12CSV airlines public dataset contains information on flight arrival and departure details for all commercial flights within the USA, from October 1987 to December 2012.</span><span class="sxs-lookup"><span data-stu-id="65872-112">The AirOnTime08to12CSV airlines public dataset contains information on flight arrival and departure details for all commercial flights within the USA, from October 1987 to December 2012.</span></span> <span data-ttu-id="65872-113">This is a large dataset: there are nearly 150 million records in total.</span><span class="sxs-lookup"><span data-stu-id="65872-113">This is a large dataset: there are nearly 150 million records in total.</span></span> <span data-ttu-id="65872-114">It is just under 4 GB unpacked.</span><span class="sxs-lookup"><span data-stu-id="65872-114">It is just under 4 GB unpacked.</span></span> <span data-ttu-id="65872-115">It is available from the [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236), and more conveniently as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from the [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span><span class="sxs-lookup"><span data-stu-id="65872-115">It is available from the [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236), and more conveniently as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from the [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span></span>

<span data-ttu-id="65872-116">To see the effects of weather on flight delays we’ll also need the weather data at each of the airports.</span><span class="sxs-lookup"><span data-stu-id="65872-116">To see the effects of weather on flight delays we’ll also need the weather data at each of the airports.</span></span> <span data-ttu-id="65872-117">This can be downloaded as zip files in raw form by month from the [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span><span class="sxs-lookup"><span data-stu-id="65872-117">This can be downloaded as zip files in raw form by month from the [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span></span> <span data-ttu-id="65872-118">For the purposes of this example we pulled weather data from May 2007 – December 2012 and used the hourly data files within each of the 68 monthly zips.</span><span class="sxs-lookup"><span data-stu-id="65872-118">For the purposes of this example we pulled weather data from May 2007 – December 2012 and used the hourly data files within each of the 68 monthly zips.</span></span> <span data-ttu-id="65872-119">The monthly zip files also contain a mapping (YYYYMMstation.txt) between the weather station ID (WBAN), the airport it’s associated with (CallSign), and the airport’s time zone offset from UTC (TimeZone) – all of which we’ll need when joining with the airline delay data.</span><span class="sxs-lookup"><span data-stu-id="65872-119">The monthly zip files also contain a mapping (YYYYMMstation.txt) between the weather station ID (WBAN), the airport it’s associated with (CallSign), and the airport’s time zone offset from UTC (TimeZone) – all of which we’ll need when joining with the airline delay data.</span></span>

## <a name="setting-up-the-spark-environment"></a><span data-ttu-id="65872-120">Setting up the Spark environment</span><span class="sxs-lookup"><span data-stu-id="65872-120">Setting up the Spark environment</span></span>

<span data-ttu-id="65872-121">We set up the Spark environment as the first step prior to preparing the weather data, and merging it with the airline data prior to modeling.</span><span class="sxs-lookup"><span data-stu-id="65872-121">We set up the Spark environment as the first step prior to preparing the weather data, and merging it with the airline data prior to modeling.</span></span> <span data-ttu-id="65872-122">We begin by pointing to the directory containing our input data directories, creating a Spark compute context, and creating a logging function for informational logging to the console:</span><span class="sxs-lookup"><span data-stu-id="65872-122">We begin by pointing to the directory containing our input data directories, creating a Spark compute context, and creating a logging function for informational logging to the console:</span></span>

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session to reduce startup times 
#   (remember to stop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

<span data-ttu-id="65872-123">Next we’ll add “Spark_Home” to the search path for R packages so we can use SparkR, and initialize a SparkR session.</span><span class="sxs-lookup"><span data-stu-id="65872-123">Next we’ll add “Spark_Home” to the search path for R packages so we can use SparkR, and initialize a SparkR session.</span></span>

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-the-weather-data"></a><span data-ttu-id="65872-124">Preparing the weather data</span><span class="sxs-lookup"><span data-stu-id="65872-124">Preparing the weather data</span></span>

<span data-ttu-id="65872-125">To prepare the weather data, we’ll subset it to the columns needed for modeling: "Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", and "Altimeter", add an airport code associated with the weather station, and convert the measurements from local time to UTC.</span><span class="sxs-lookup"><span data-stu-id="65872-125">To prepare the weather data, we’ll subset it to the columns needed for modeling: "Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", and "Altimeter", add an airport code associated with the weather station, and convert the measurements from local time to UTC.</span></span>

<span data-ttu-id="65872-126">We begin by creating a file to map the weather station (WBAN) info to an airport code.</span><span class="sxs-lookup"><span data-stu-id="65872-126">We begin by creating a file to map the weather station (WBAN) info to an airport code.</span></span> <span data-ttu-id="65872-127">We could get this from the mapping file included with the weather data by mapping the CallSign (e.g. LAX) field in the weather data file to Origin in the airline data, however we just happened to have another mapping on hand that maps WBAN to AirportID (e.g. 12892 for LAX) and includes TimeZone that has been saved to a CSV file called “wban-to-airport-id-tz.CSV” that we’ll use, e.g.</span><span class="sxs-lookup"><span data-stu-id="65872-127">We could get this from the mapping file included with the weather data by mapping the CallSign (e.g. LAX) field in the weather data file to Origin in the airline data, however we just happened to have another mapping on hand that maps WBAN to AirportID (e.g. 12892 for LAX) and includes TimeZone that has been saved to a CSV file called “wban-to-airport-id-tz.CSV” that we’ll use, e.g.</span></span>

| <span data-ttu-id="65872-128">AirportID</span><span class="sxs-lookup"><span data-stu-id="65872-128">AirportID</span></span> | <span data-ttu-id="65872-129">WBAN</span><span class="sxs-lookup"><span data-stu-id="65872-129">WBAN</span></span> | <span data-ttu-id="65872-130">TimeZone</span><span class="sxs-lookup"><span data-stu-id="65872-130">TimeZone</span></span>
|-----------|------|---------
| <span data-ttu-id="65872-131">10685</span><span class="sxs-lookup"><span data-stu-id="65872-131">10685</span></span> | <span data-ttu-id="65872-132">54831</span><span class="sxs-lookup"><span data-stu-id="65872-132">54831</span></span> | <span data-ttu-id="65872-133">-6</span><span class="sxs-lookup"><span data-stu-id="65872-133">-6</span></span>
| <span data-ttu-id="65872-134">14871</span><span class="sxs-lookup"><span data-stu-id="65872-134">14871</span></span> | <span data-ttu-id="65872-135">24232</span><span class="sxs-lookup"><span data-stu-id="65872-135">24232</span></span> | <span data-ttu-id="65872-136">-8</span><span class="sxs-lookup"><span data-stu-id="65872-136">-8</span></span>
| <span data-ttu-id="65872-137">..</span><span class="sxs-lookup"><span data-stu-id="65872-137">..</span></span> | <span data-ttu-id="65872-138">..</span><span class="sxs-lookup"><span data-stu-id="65872-138">..</span></span> | <span data-ttu-id="65872-139">..</span><span class="sxs-lookup"><span data-stu-id="65872-139">..</span></span>

<span data-ttu-id="65872-140">The following code reads each of the hourly raw weather data files, subsets to the columns we’ll need, merges the weather station mapping file, adjusts the date times of measurements to UTC, and then writes out a new version of the file.</span><span class="sxs-lookup"><span data-stu-id="65872-140">The following code reads each of the hourly raw weather data files, subsets to the columns we’ll need, merges the weather station mapping file, adjusts the date times of measurements to UTC, and then writes out a new version of the file.</span></span>

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-the-airline-and-weather-data-to-spark-dataframes"></a><span data-ttu-id="65872-141">Importing the airline and weather data to Spark DataFrames</span><span class="sxs-lookup"><span data-stu-id="65872-141">Importing the airline and weather data to Spark DataFrames</span></span>

<span data-ttu-id="65872-142">Now we’ll use the SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function to import the weather and airline data to Spark DataFrames.</span><span class="sxs-lookup"><span data-stu-id="65872-142">Now we’ll use the SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function to import the weather and airline data to Spark DataFrames.</span></span> <span data-ttu-id="65872-143">Note that this function, like many other Spark methods, are lazily executed, meaning that they are queued for execution but not actually executed until required.</span><span class="sxs-lookup"><span data-stu-id="65872-143">Note that this function, like many other Spark methods, are lazily executed, meaning that they are queued for execution but not actually executed until required.</span></span>

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for the airline data

logmsg('create a SparkR DataFrame for the airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for the weather data

logmsg('create a SparkR DataFrame for the weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a><span data-ttu-id="65872-144">Data cleansing and transformation</span><span class="sxs-lookup"><span data-stu-id="65872-144">Data cleansing and transformation</span></span>

<span data-ttu-id="65872-145">Next we’ll do some cleanup on the airline data we’ve imported to rename columns, only keep the variables we need, and round scheduled departure times down to the nearest hour to enable merging with the latest weather data prior to departure.</span><span class="sxs-lookup"><span data-stu-id="65872-145">Next we’ll do some cleanup on the airline data we’ve imported to rename columns, only keep the variables we need, and round scheduled departure times down to the nearest hour to enable merging with the latest weather data prior to departure.</span></span>

```
logmsg('clean the airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from the flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time to full hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

<span data-ttu-id="65872-146">Now we‘ll perform similar operations on the weather data:</span><span class="sxs-lookup"><span data-stu-id="65872-146">Now we‘ll perform similar operations on the weather data:</span></span>

```
# Average weather readings by hour
logmsg('clean the weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-the-weather-and-airline-data"></a><span data-ttu-id="65872-147">Joining the weather and airline data</span><span class="sxs-lookup"><span data-stu-id="65872-147">Joining the weather and airline data</span></span>

<span data-ttu-id="65872-148">We’ll now use the SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function to do a left outer join of the airline and weather data by departure AirportID and datetime.</span><span class="sxs-lookup"><span data-stu-id="65872-148">We’ll now use the SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function to do a left outer join of the airline and weather data by departure AirportID and datetime.</span></span> <span data-ttu-id="65872-149">The outer join allows us to retain all the airline data records even if there is no matching weather data.</span><span class="sxs-lookup"><span data-stu-id="65872-149">The outer join allows us to retain all the airline data records even if there is no matching weather data.</span></span> <span data-ttu-id="65872-150">Following the join, we’ll remove some redundant columns, and rename the kept columns to remove the incoming DataFrame prefix introduced by the join.</span><span class="sxs-lookup"><span data-stu-id="65872-150">Following the join, we’ll remove some redundant columns, and rename the kept columns to remove the incoming DataFrame prefix introduced by the join.</span></span>

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

<span data-ttu-id="65872-151">In a similar fashion, we’ll join the weather and airline data based on arrival AirportID and datetime.</span><span class="sxs-lookup"><span data-stu-id="65872-151">In a similar fashion, we’ll join the weather and airline data based on arrival AirportID and datetime.</span></span>

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-to-csv-for-exchange-with-scaler"></a><span data-ttu-id="65872-152">Save results to CSV for exchange with ScaleR</span><span class="sxs-lookup"><span data-stu-id="65872-152">Save results to CSV for exchange with ScaleR</span></span>

<span data-ttu-id="65872-153">That completes the joins we need to do so we’re done with SparkR.</span><span class="sxs-lookup"><span data-stu-id="65872-153">That completes the joins we need to do so we’re done with SparkR.</span></span> <span data-ttu-id="65872-154">We’ll save the data from the final Spark DataFrame “joinedDF5” to a CSV for input to ScaleR and then close out the SparkR session.</span><span class="sxs-lookup"><span data-stu-id="65872-154">We’ll save the data from the final Spark DataFrame “joinedDF5” to a CSV for input to ScaleR and then close out the SparkR session.</span></span> <span data-ttu-id="65872-155">We explicitly tell SparkR to save the resultant CSV in 80 separate partitions to enable sufficient parallelism in ScaleR processing.</span><span class="sxs-lookup"><span data-stu-id="65872-155">We explicitly tell SparkR to save the resultant CSV in 80 separate partitions to enable sufficient parallelism in ScaleR processing.</span></span>

```
logmsg('output the joined data from Spark to CSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result to directory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down the SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-to-xdf-for-use-by-scaler"></a><span data-ttu-id="65872-156">Import to XDF for use by ScaleR</span><span class="sxs-lookup"><span data-stu-id="65872-156">Import to XDF for use by ScaleR</span></span>

<span data-ttu-id="65872-157">We could use the CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source, but we’ll import it to XDF since it is more efficient when running multiple operations on the dataset.</span><span class="sxs-lookup"><span data-stu-id="65872-157">We could use the CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source, but we’ll import it to XDF since it is more efficient when running multiple operations on the dataset.</span></span>

```
logmsg('Import the CSV to compressed, binary XDF format') 

# set the Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a><span data-ttu-id="65872-158">Splitting data for training and test</span><span class="sxs-lookup"><span data-stu-id="65872-158">Splitting data for training and test</span></span>

<span data-ttu-id="65872-159">We use rxDataStep to split out the 2012 data for testing and keep the rest for training.</span><span class="sxs-lookup"><span data-stu-id="65872-159">We use rxDataStep to split out the 2012 data for testing and keep the rest for training.</span></span>

```
# split out the training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out the testing data

logmsg('split out the test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a><span data-ttu-id="65872-160">Train and test a logistic regression model</span><span class="sxs-lookup"><span data-stu-id="65872-160">Train and test a logistic regression model</span></span>

<span data-ttu-id="65872-161">OK, we’re ready to build a model!</span><span class="sxs-lookup"><span data-stu-id="65872-161">OK, we’re ready to build a model!</span></span> <span data-ttu-id="65872-162">To see the influence of weather data on delay in the arrival time we’ll use ScaleR’s logistic regression routine to model whether an arrival delay of greater than 15 minutes is influenced by relative date, departure and arrival airports, and the weather at the departure and arrival airports, etc.</span><span class="sxs-lookup"><span data-stu-id="65872-162">To see the influence of weather data on delay in the arrival time we’ll use ScaleR’s logistic regression routine to model whether an arrival delay of greater than 15 minutes is influenced by relative date, departure and arrival airports, and the weather at the departure and arrival airports, etc.</span></span>

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use the scalable rxLogit() function but set max iterations to 3 for the purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

<span data-ttu-id="65872-163">Now let’s see how it does on the test data by making some predictions and looking at ROC and AUC.</span><span class="sxs-lookup"><span data-stu-id="65872-163">Now let’s see how it does on the test data by making some predictions and looking at ROC and AUC.</span></span>

```
# Predict over test data (Logistic Regression).

logmsg('predict over the test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use the scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under the Curve (AUC).

logmsg('calculate the roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a><span data-ttu-id="65872-164">Scoring elsewhere</span><span class="sxs-lookup"><span data-stu-id="65872-164">Scoring elsewhere</span></span>

<span data-ttu-id="65872-165">We can also use the model for scoring data on another platform by saving it to an RDS file and then transferring and importing that RDS into the destination scoring environment such as SQL Server R Services.</span><span class="sxs-lookup"><span data-stu-id="65872-165">We can also use the model for scoring data on another platform by saving it to an RDS file and then transferring and importing that RDS into the destination scoring environment such as SQL Server R Services.</span></span> <span data-ttu-id="65872-166">When doing so, it’s important to ensure that the factor levels of the data to be scored match those on which the model was built.</span><span class="sxs-lookup"><span data-stu-id="65872-166">When doing so, it’s important to ensure that the factor levels of the data to be scored match those on which the model was built.</span></span> <span data-ttu-id="65872-167">That can be achieved by extracting and saving the column info associated with the modeling data via ScaleR’s rxCreateColInfo() function, and then applying that column info to the input data source for prediction.</span><span class="sxs-lookup"><span data-stu-id="65872-167">That can be achieved by extracting and saving the column info associated with the modeling data via ScaleR’s rxCreateColInfo() function, and then applying that column info to the input data source for prediction.</span></span> <span data-ttu-id="65872-168">In the following we just save a few rows of the test dataset and will extract and use the column info from this sample in the prediction script.</span><span class="sxs-lookup"><span data-stu-id="65872-168">In the following we just save a few rows of the test dataset and will extract and use the column info from this sample in the prediction script.</span></span>

```
# save the model and a sample of the test dataset 

logmsg('save serialized version of the model and a sample of the test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop the spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a><span data-ttu-id="65872-169">Summary</span><span class="sxs-lookup"><span data-stu-id="65872-169">Summary</span></span>

<span data-ttu-id="65872-170">That’s it!</span><span class="sxs-lookup"><span data-stu-id="65872-170">That’s it!</span></span> <span data-ttu-id="65872-171">In this article, we’ve shown how it’s possible to combine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark so long as you remember to maintain separate Spark sessions, only run one session at a time, and exchange data via CSV files.</span><span class="sxs-lookup"><span data-stu-id="65872-171">In this article, we’ve shown how it’s possible to combine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark so long as you remember to maintain separate Spark sessions, only run one session at a time, and exchange data via CSV files.</span></span> <span data-ttu-id="65872-172">Although straightforward, this process will get a whole lot easier in an upcoming R Server release when SparkR and ScaleR can share a Spark session and thereby Spark DataFrames.</span><span class="sxs-lookup"><span data-stu-id="65872-172">Although straightforward, this process will get a whole lot easier in an upcoming R Server release when SparkR and ScaleR can share a Spark session and thereby Spark DataFrames.</span></span>

## <a name="next-steps-and-more-information"></a><span data-ttu-id="65872-173">Next steps and more information</span><span class="sxs-lookup"><span data-stu-id="65872-173">Next steps and more information</span></span>

- <span data-ttu-id="65872-174">For more information on use of R Server on Spark see the [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span><span class="sxs-lookup"><span data-stu-id="65872-174">For more information on use of R Server on Spark see the [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span></span>

- <span data-ttu-id="65872-175">For general information on R Server see the [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span><span class="sxs-lookup"><span data-stu-id="65872-175">For general information on R Server see the [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span></span>

- <span data-ttu-id="65872-176">Other articles of interest are [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md) and [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65872-176">Other articles of interest are [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md) and [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md).</span></span>

<span data-ttu-id="65872-177">For more information on use of SparkR see the following:</span><span class="sxs-lookup"><span data-stu-id="65872-177">For more information on use of SparkR see the following:</span></span>

- [<span data-ttu-id="65872-178">Apache SparkR document</span><span class="sxs-lookup"><span data-stu-id="65872-178">Apache SparkR document</span></span>](https://spark.apache.org/docs/2.1.0/sparkr.html)

- <span data-ttu-id="65872-179">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span><span class="sxs-lookup"><span data-stu-id="65872-179">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span></span>
