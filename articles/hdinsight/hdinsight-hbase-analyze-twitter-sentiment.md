---
title: Analyze real-time Twitter sentiment with HBase | Microsoft Docs
description: Learn how to do real-time sentiment analysis of big data from Twitter using HBase in an HDInsight (Hadoop) cluster.
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5c798ad3-a20d-4385-a463-f4f7705f9566
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: jgao
ms.openlocfilehash: a735fc9d89bd2f65c407c4cf392e009259cf5712
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555978"
---
# <a name="analyze-real-time-twitter-sentiment-with-hbase-in-hdinsight"></a><span data-ttu-id="da23a-103">Analyze real-time Twitter sentiment with HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="da23a-103">Analyze real-time Twitter sentiment with HBase in HDInsight</span></span>
<span data-ttu-id="da23a-104">Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data from Twitter by using a HBase cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da23a-104">Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data from Twitter by using a HBase cluster in HDInsight.</span></span>

<span data-ttu-id="da23a-105">Social websites are one of the major driving forces for big data adoption.</span><span class="sxs-lookup"><span data-stu-id="da23a-105">Social websites are one of the major driving forces for big data adoption.</span></span> <span data-ttu-id="da23a-106">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span><span class="sxs-lookup"><span data-stu-id="da23a-106">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span> <span data-ttu-id="da23a-107">In this tutorial, you will develop a console streaming service application and an ASP.NET web application to perform the following:</span><span class="sxs-lookup"><span data-stu-id="da23a-107">In this tutorial, you will develop a console streaming service application and an ASP.NET web application to perform the following:</span></span>

![HDInsight HBase Analyze Twitter sentiment][img-app-arch]

* <span data-ttu-id="da23a-109">The streaming application</span><span class="sxs-lookup"><span data-stu-id="da23a-109">The streaming application</span></span>

  * <span data-ttu-id="da23a-110">get geo-tagged tweets in real time by using the Twitter streaming API</span><span class="sxs-lookup"><span data-stu-id="da23a-110">get geo-tagged tweets in real time by using the Twitter streaming API</span></span>
  * <span data-ttu-id="da23a-111">evaluate the sentiment of these tweets</span><span class="sxs-lookup"><span data-stu-id="da23a-111">evaluate the sentiment of these tweets</span></span>
  * <span data-ttu-id="da23a-112">store the sentiment information in HBase by using the Microsoft HBase SDK</span><span class="sxs-lookup"><span data-stu-id="da23a-112">store the sentiment information in HBase by using the Microsoft HBase SDK</span></span>
* <span data-ttu-id="da23a-113">The Azure Websites application</span><span class="sxs-lookup"><span data-stu-id="da23a-113">The Azure Websites application</span></span>

  * <span data-ttu-id="da23a-114">plot the real-time statistical results on Bing maps by using an ASP.NET web application.</span><span class="sxs-lookup"><span data-stu-id="da23a-114">plot the real-time statistical results on Bing maps by using an ASP.NET web application.</span></span> <span data-ttu-id="da23a-115">A visualization of the tweets will look something like this:</span><span class="sxs-lookup"><span data-stu-id="da23a-115">A visualization of the tweets will look something like this:</span></span>

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]

    <span data-ttu-id="da23a-117">You will be able to query tweets with certain keywords to get a sense of if the expressed opinion in the tweets is positive, negative, or neutral.</span><span class="sxs-lookup"><span data-stu-id="da23a-117">You will be able to query tweets with certain keywords to get a sense of if the expressed opinion in the tweets is positive, negative, or neutral.</span></span>

<span data-ttu-id="da23a-118">A complete Visual Studio solution sample can be found on GitHub: [Realtime social sentiment analysis app](https://github.com/maxluk/tweet-sentiment).</span><span class="sxs-lookup"><span data-stu-id="da23a-118">A complete Visual Studio solution sample can be found on GitHub: [Realtime social sentiment analysis app](https://github.com/maxluk/tweet-sentiment).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="da23a-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="da23a-119">Prerequisites</span></span>
<span data-ttu-id="da23a-120">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="da23a-120">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="da23a-121">**An HBase cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="da23a-121">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="da23a-122">For instructions about creating clusters, see  [Get started using HBase with Hadoop in HDInsight][hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="da23a-122">For instructions about creating clusters, see  [Get started using HBase with Hadoop in HDInsight][hbase-get-started].</span></span> <span data-ttu-id="da23a-123">You will need the following data to go through the tutorial:</span><span class="sxs-lookup"><span data-stu-id="da23a-123">You will need the following data to go through the tutorial:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="da23a-124">Cluster property</span><span class="sxs-lookup"><span data-stu-id="da23a-124">Cluster property</span></span></th><th><span data-ttu-id="da23a-125">Description</span><span class="sxs-lookup"><span data-stu-id="da23a-125">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="da23a-126">HBase cluster name</span><span class="sxs-lookup"><span data-stu-id="da23a-126">HBase cluster name</span></span></td><td><span data-ttu-id="da23a-127">Your HDInsight HBase cluster name.</span><span class="sxs-lookup"><span data-stu-id="da23a-127">Your HDInsight HBase cluster name.</span></span> <span data-ttu-id="da23a-128">For example: https://myhbase.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="da23a-128">For example: https://myhbase.azurehdinsight.net/</span></span></td></tr>
    <tr><td><span data-ttu-id="da23a-129">Cluster user name</span><span class="sxs-lookup"><span data-stu-id="da23a-129">Cluster user name</span></span></td><td><span data-ttu-id="da23a-130">The Hadoop user account name.</span><span class="sxs-lookup"><span data-stu-id="da23a-130">The Hadoop user account name.</span></span> <span data-ttu-id="da23a-131">The default Hadoop user name is <strong>admin</strong>.</span><span class="sxs-lookup"><span data-stu-id="da23a-131">The default Hadoop user name is <strong>admin</strong>.</span></span></td></tr>
    <tr><td><span data-ttu-id="da23a-132">Cluster user password</span><span class="sxs-lookup"><span data-stu-id="da23a-132">Cluster user password</span></span></td><td><span data-ttu-id="da23a-133">The Hadoop cluster user password.</span><span class="sxs-lookup"><span data-stu-id="da23a-133">The Hadoop cluster user password.</span></span></td></tr>
    </table>

* <span data-ttu-id="da23a-134">**A workstation** with Visual Studio 2013/2015/2017 installed.</span><span class="sxs-lookup"><span data-stu-id="da23a-134">**A workstation** with Visual Studio 2013/2015/2017 installed.</span></span> <span data-ttu-id="da23a-135">For instructions, see [Installing Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).</span><span class="sxs-lookup"><span data-stu-id="da23a-135">For instructions, see [Installing Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).</span></span>

## <a name="create-a-twitter-application-id-and-secrets"></a><span data-ttu-id="da23a-136">Create a Twitter application ID and secrets</span><span class="sxs-lookup"><span data-stu-id="da23a-136">Create a Twitter application ID and secrets</span></span>
<span data-ttu-id="da23a-137">The Twitter streaming APIs use [OAuth](http://oauth.net/) to authorize requests.</span><span class="sxs-lookup"><span data-stu-id="da23a-137">The Twitter streaming APIs use [OAuth](http://oauth.net/) to authorize requests.</span></span> <span data-ttu-id="da23a-138">The first step to use OAuth is to create a new application on the Twitter developer site.</span><span class="sxs-lookup"><span data-stu-id="da23a-138">The first step to use OAuth is to create a new application on the Twitter developer site.</span></span>

<span data-ttu-id="da23a-139">**To create Twitter application ID and secrets**</span><span class="sxs-lookup"><span data-stu-id="da23a-139">**To create Twitter application ID and secrets**</span></span>

1. <span data-ttu-id="da23a-140">Sign in to [Twitter Apps](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="da23a-140">Sign in to [Twitter Apps](https://apps.twitter.com/).</span></span> <span data-ttu-id="da23a-141">Click the **Sign up now** link if you don't have a Twitter account.</span><span class="sxs-lookup"><span data-stu-id="da23a-141">Click the **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="da23a-142">Click **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="da23a-142">Click **Create New App**.</span></span>
3. <span data-ttu-id="da23a-143">Enter a **Name**, **Description**, and **Website**.</span><span class="sxs-lookup"><span data-stu-id="da23a-143">Enter a **Name**, **Description**, and **Website**.</span></span> <span data-ttu-id="da23a-144">The Twitter application name must be a unique name.</span><span class="sxs-lookup"><span data-stu-id="da23a-144">The Twitter application name must be a unique name.</span></span> <span data-ttu-id="da23a-145">The Website field is not really used.</span><span class="sxs-lookup"><span data-stu-id="da23a-145">The Website field is not really used.</span></span> <span data-ttu-id="da23a-146">It doesn't have to be a valid URL.</span><span class="sxs-lookup"><span data-stu-id="da23a-146">It doesn't have to be a valid URL.</span></span>
4. <span data-ttu-id="da23a-147">Check **Yes, I agree**, and then click **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="da23a-147">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="da23a-148">Click the **Permissions** tab. The default permission is **Read only**.</span><span class="sxs-lookup"><span data-stu-id="da23a-148">Click the **Permissions** tab. The default permission is **Read only**.</span></span> <span data-ttu-id="da23a-149">This is sufficient for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="da23a-149">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="da23a-150">Click the **Keys and Access Tokens** tab.</span><span class="sxs-lookup"><span data-stu-id="da23a-150">Click the **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="da23a-151">Click **Create my access token**.</span><span class="sxs-lookup"><span data-stu-id="da23a-151">Click **Create my access token**.</span></span>
8. <span data-ttu-id="da23a-152">Click **Test OAuth** in the upper-right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="da23a-152">Click **Test OAuth** in the upper-right corner of the page.</span></span>
9. <span data-ttu-id="da23a-153">Copy the **Consumer key**, **Consumer secret**, **Access token**, and **Access token secret** values.</span><span class="sxs-lookup"><span data-stu-id="da23a-153">Copy the **Consumer key**, **Consumer secret**, **Access token**, and **Access token secret** values.</span></span> <span data-ttu-id="da23a-154">You will need these values later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="da23a-154">You will need these values later in the tutorial.</span></span>

    ![hdi.hbase.twitter.sentiment.twitter.app][img-twitter-app]

## <a name="create-twitter-streaming-service"></a><span data-ttu-id="da23a-156">Create Twitter streaming service</span><span class="sxs-lookup"><span data-stu-id="da23a-156">Create Twitter streaming service</span></span>
<span data-ttu-id="da23a-157">You need to create an application to get tweets, calculate tweet sentiment score, and send the processed tweet words to HBase.</span><span class="sxs-lookup"><span data-stu-id="da23a-157">You need to create an application to get tweets, calculate tweet sentiment score, and send the processed tweet words to HBase.</span></span>

<span data-ttu-id="da23a-158">**To create the streaming application**</span><span class="sxs-lookup"><span data-stu-id="da23a-158">**To create the streaming application**</span></span>

1. <span data-ttu-id="da23a-159">Open **Visual Studio**, and create a Visual C# console application called **TweetSentimentStreaming**.</span><span class="sxs-lookup"><span data-stu-id="da23a-159">Open **Visual Studio**, and create a Visual C# console application called **TweetSentimentStreaming**.</span></span>
2. <span data-ttu-id="da23a-160">From **Package Manager Console**, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="da23a-160">From **Package Manager Console**, run the following commands:</span></span>

        Install-Package Microsoft.HBase.Client -version 0.4.2.0
        Install-Package TweetinviAPI -version 1.0.0.0

    <span data-ttu-id="da23a-161">These commands install the [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) package, which is the client library to access the HBase cluster, and the [Tweetinvi API](https://www.nuget.org/packages/TweetinviAPI/) package, which is used to access the Twitter API.</span><span class="sxs-lookup"><span data-stu-id="da23a-161">These commands install the [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) package, which is the client library to access the HBase cluster, and the [Tweetinvi API](https://www.nuget.org/packages/TweetinviAPI/) package, which is used to access the Twitter API.</span></span>

   > [!NOTE]
   > <span data-ttu-id="da23a-162">The sample used in this article has been tested using the version specified above.</span><span class="sxs-lookup"><span data-stu-id="da23a-162">The sample used in this article has been tested using the version specified above.</span></span>  <span data-ttu-id="da23a-163">You can remove the -version switch to install the latest version.</span><span class="sxs-lookup"><span data-stu-id="da23a-163">You can remove the -version switch to install the latest version.</span></span>
   >
   >
3. <span data-ttu-id="da23a-164">From **Solution Explorer**, add **System.Configuration** to the reference.</span><span class="sxs-lookup"><span data-stu-id="da23a-164">From **Solution Explorer**, add **System.Configuration** to the reference.</span></span>
4. <span data-ttu-id="da23a-165">Add a new class file to the project called **HBaseWriter.cs**, and then replace the code with the following:</span><span class="sxs-lookup"><span data-stu-id="da23a-165">Add a new class file to the project called **HBaseWriter.cs**, and then replace the code with the following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Text;
        using System.Threading;
        using Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling;
        using org.apache.hadoop.hbase.rest.protobuf.generated;
        using Microsoft.HBase.Client;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class HBaseWriter
            {
                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "https://<Enter Your Cluster Name>.azurehdinsight.net/";
                const string HADOOPUSERNAME = "admin"; //the default name is "admin"
                const string HADOOPUSERPASSWORD = "<Enter the Hadoop User Password>";

                const string HBASETABLENAME = "tweets_by_words";
                const string COUNT_ROW_KEY = "~ROWCOUNT";
                const string COUNT_COLUMN_NAME = "d:COUNT";

                long rowCount = 0;

                // Sentiment dictionary file and the punctuation characters
                const string DICTIONARYFILENAME = @"..\..\dictionary.tsv";
                private static char[] _punctuationChars = new[] {
            ' ', '!', '\"', '#', '$', '%', '&', '\'', '(', ')', '*', '+', ',', '-', '.', '/',   //ascii 23--47
            ':', ';', '<', '=', '>', '?', '@', '[', ']', '^', '_', '`', '{', '|', '}', '~' };   //ascii 58--64 + misc.

                // For writting to HBase
                HBaseClient client;

                // a sentiment dictionary for estimate sentiment. It is loaded from a physical file.
                Dictionary<string, DictionaryItem> dictionary;

                // use multithread write
                Thread writerThread;
                Queue<ITweet> queue = new Queue<ITweet>();
                bool threadRunning = true;

                // This function connects to HBase, loads the sentiment dictionary, and starts the thread for writting.
                public HBaseWriter()
                {
                    ClusterCredentials credentials = new ClusterCredentials(new Uri(CLUSTERNAME), HADOOPUSERNAME, HADOOPUSERPASSWORD);
                    client = new HBaseClient(credentials);

                    // create the HBase table if it doesn't exist
                    if (!client.ListTablesAsync().Result.name.Contains(HBASETABLENAME))
                    {
                        TableSchema tableSchema = new TableSchema();
                        tableSchema.name = HBASETABLENAME;
                        tableSchema.columns.Add(new ColumnSchema { name = "d" });
                        client.CreateTableAsync(tableSchema).Wait();
                        Console.WriteLine("Table \"{0}\" is created.", HBASETABLENAME);
                    }

                    // Read current row count cell
                    rowCount = GetRowCount();

                    // Load sentiment dictionary from a file
                    LoadDictionary();

                    // Start a thread for writting to HBase
                    writerThread = new Thread(new ThreadStart(WriterThreadFunction));
                    writerThread.Start();
                }

                ~HBaseWriter()
                {
                    threadRunning = false;
                }

                private long GetRowCount()
                {
                    try
                    {
                        RequestOptions options = RequestOptions.GetDefaultOptions();
                        options.RetryPolicy = RetryPolicy.NoRetry;
                        var cellSet = client.GetCellsAsync(HBASETABLENAME, COUNT_ROW_KEY, null, null, options).Result;
                        if (cellSet.rows.Count != 0)
                        {
                            var countCol = cellSet.rows[0].values.Find(cell => Encoding.UTF8.GetString(cell.column) == COUNT_COLUMN_NAME);
                            if (countCol != null)
                            {
                                return Convert.ToInt64(Encoding.UTF8.GetString(countCol.data));
                            }
                        }
                    }
                    catch(Exception ex)
                    {
                        if (ex.InnerException.Message.Equals("The remote server returned an error: (404) Not Found.", StringComparison.OrdinalIgnoreCase))
                        {
                            return 0;
                        }
                        else
                        {
                            throw ex;
                        }

                    }

                    return 0;
                }

                // Enqueue the Tweets received
                public void WriteTweet(ITweet tweet)
                {
                    lock (queue)
                    {
                        queue.Enqueue(tweet);
                    }
                }

                // Load sentiment dictionary from a file
                private void LoadDictionary()
                {
                    List<string> lines = File.ReadAllLines(DICTIONARYFILENAME).ToList();
                    var items = lines.Select(line =>
                    {
                        var fields = line.Split('\t');
                        var pos = 0;
                        return new DictionaryItem
                        {
                            Type = fields[pos++],
                            Length = Convert.ToInt32(fields[pos++]),
                            Word = fields[pos++],
                            Pos = fields[pos++],
                            Stemmed = fields[pos++],
                            Polarity = fields[pos++]
                        };
                    });

                    dictionary = new Dictionary<string, DictionaryItem>();
                    foreach (var item in items)
                    {
                        if (!dictionary.Keys.Contains(item.Word))
                        {
                            dictionary.Add(item.Word, item);
                        }
                    }
                }

                // Calculate sentiment score
                private int CalcSentimentScore(string[] words)
                {
                    Int32 total = 0;
                    foreach (string word in words)
                    {
                        if (dictionary.Keys.Contains(word))
                        {
                            switch (dictionary[word].Polarity)
                            {
                                case "negative": total -= 1; break;
                                case "positive": total += 1; break;
                            }
                        }
                    }
                    if (total > 0)
                    {
                        return 1;
                    }
                    else if (total < 0)
                    {
                        return -1;
                    }
                    else
                    {
                        return 0;
                    }
                }

                // Popular a CellSet object to be written into HBase
                private void CreateTweetByWordsCells(CellSet set, ITweet tweet)
                {
                    // Split the Tweet into words
                    string[] words = tweet.Text.ToLower().Split(_punctuationChars);

                    // Calculate sentiment score base on the words
                    int sentimentScore = CalcSentimentScore(words);
                    var word_pairs = words.Take(words.Length - 1)
                                        .Select((word, idx) => string.Format("{0} {1}", word, words[idx + 1]));
                    var all_words = words.Concat(word_pairs).ToList();

                    // For each word in the Tweet add a row to the HBase table
                    foreach (string word in all_words)
                    {
                        string time_index = (ulong.MaxValue - (ulong)tweet.CreatedAt.ToBinary()).ToString().PadLeft(20) + tweet.IdStr;
                        string key = word + "_" + time_index;

                        // Create a row
                        var row = new CellSet.Row { key = Encoding.UTF8.GetBytes(key) };

                        // Add columns to the row, including Tweet identifier, language, coordinator(if available), and sentiment
                        var value = new Cell { column = Encoding.UTF8.GetBytes("d:id_str"), data = Encoding.UTF8.GetBytes(tweet.IdStr) };
                        row.values.Add(value);

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:lang"), data = Encoding.UTF8.GetBytes(tweet.Language.ToString()) };
                        row.values.Add(value);

                        if (tweet.Coordinates != null)
                        {
                            var str = tweet.Coordinates.Longitude.ToString() + "," + tweet.Coordinates.Latitude.ToString();
                            value = new Cell { column = Encoding.UTF8.GetBytes("d:coor"), data = Encoding.UTF8.GetBytes(str) };
                            row.values.Add(value);
                        }

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:sentiment"), data = Encoding.UTF8.GetBytes(sentimentScore.ToString()) };
                        row.values.Add(value);

                        set.rows.Add(row);
                    }
                }

                // Write a Tweet (CellSet) to HBase
                public void WriterThreadFunction()
                {
                    try
                    {
                        while (threadRunning)
                        {
                            if (queue.Count > 0)
                            {
                                CellSet set = new CellSet();
                                lock (queue)
                                {
                                    do
                                    {
                                        ITweet tweet = queue.Dequeue();
                                        CreateTweetByWordsCells(set, tweet);
                                    } while (queue.Count > 0);
                                }

                                // Write the Tweet by words cell set to the HBase table
                                client.StoreCellsAsync(HBASETABLENAME, set).Wait();
                                Console.WriteLine("\tRows written: {0}", set.rows.Count);
                            }
                            Thread.Sleep(100);
                        }
                    }
                    catch (Exception ex)
                    {
                        Console.WriteLine("Exception: " + ex.Message);
                    }
                }
            }
            public class DictionaryItem
            {
                public string Type { get; set; }
                public int Length { get; set; }
                public string Word { get; set; }
                public string Pos { get; set; }
                public string Stemmed { get; set; }
                public string Polarity { get; set; }
            }
        }
5. <span data-ttu-id="da23a-166">Set the constants in the previous code, including **CLUSTERNAME**, **HADOOPUSERNAME**, **HADOOPUSERPASSWORD**, and DICTIONARYFILENAME.</span><span class="sxs-lookup"><span data-stu-id="da23a-166">Set the constants in the previous code, including **CLUSTERNAME**, **HADOOPUSERNAME**, **HADOOPUSERPASSWORD**, and DICTIONARYFILENAME.</span></span> <span data-ttu-id="da23a-167">The DICTIONARYFILENAME is the filename and the location of the direction.tsv.</span><span class="sxs-lookup"><span data-stu-id="da23a-167">The DICTIONARYFILENAME is the filename and the location of the direction.tsv.</span></span>  <span data-ttu-id="da23a-168">The file can be downloaded from **https://hditutorialdata.blob.core.windows.net/twittersentiment/dictionary.tsv**.</span><span class="sxs-lookup"><span data-stu-id="da23a-168">The file can be downloaded from **https://hditutorialdata.blob.core.windows.net/twittersentiment/dictionary.tsv**.</span></span> <span data-ttu-id="da23a-169">If you want to change the HBase table name, you must change the table name in the web application accordingly.</span><span class="sxs-lookup"><span data-stu-id="da23a-169">If you want to change the HBase table name, you must change the table name in the web application accordingly.</span></span>
6. <span data-ttu-id="da23a-170">Open **Program.cs**, and replace the code with the following:</span><span class="sxs-lookup"><span data-stu-id="da23a-170">Open **Program.cs**, and replace the code with the following:</span></span>

        using System;
        using System.Diagnostics;
        using Tweetinvi;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class Program
            {
                const string TWITTERAPPACCESSTOKEN = "<Enter Twitter App Access Token>";
                const string TWITTERAPPACCESSTOKENSECRET = "<Enter Twitter Access Token Secret>";
                const string TWITTERAPPAPIKEY = "<Enter Twitter App API Key>";
                const string TWITTERAPPAPISECRET = "<Enter Twitter App API Secret>";

                static void Main(string[] args)
                {
                    Auth.SetUserCredentials(TWITTERAPPAPIKEY, TWITTERAPPAPISECRET, TWITTERAPPACCESSTOKEN, TWITTERAPPACCESSTOKENSECRET);

                    Stream_FilteredStreamExample();
                }

                private static void Stream_FilteredStreamExample()
                {
                    for (;;)
                    {
                        try
                        {
                            HBaseWriter hbase = new HBaseWriter();
                            var stream = Stream.CreateFilteredStream();
                            stream.AddLocation(new Coordinates(-180, -90), new Coordinates(180, 90));

                            var tweetCount = 0;
                            var timer = Stopwatch.StartNew();

                            stream.MatchingTweetReceived += (sender, args) =>
                            {
                                tweetCount++;
                                var tweet = args.Tweet;

                                // Write Tweets to HBase
                                hbase.WriteTweet(tweet);

                                if (timer.ElapsedMilliseconds > 1000)
                                {
                                    if (tweet.Coordinates != null)
                                    {
                                        Console.ForegroundColor = ConsoleColor.Green;
                                        Console.WriteLine("\n{0}: {1} {2}", tweet.Id, tweet.Language.ToString(), tweet.Text);
                                        Console.ForegroundColor = ConsoleColor.White;
                                        Console.WriteLine("\tLocation: {0}, {1}", tweet.Coordinates.Longitude, tweet.Coordinates.Latitude);
                                    }

                                    timer.Restart();
                                    Console.WriteLine("\tTweets/sec: {0}", tweetCount);
                                    tweetCount = 0;
                                }
                            };

                            stream.StartStreamMatchingAllConditions();
                        }
                        catch (Exception ex)
                        {
                            Console.WriteLine("Exception: {0}", ex.Message);
                        }
                    }
                }

            }
        }
7. <span data-ttu-id="da23a-171">Set the constants including **TWITTERAPPACCESSTOKEN**, **TWITTERAPPACCESSTOKENSECRET**, **TWITTERAPPAPIKEY** and **TWITTERAPPAPISECRET**.</span><span class="sxs-lookup"><span data-stu-id="da23a-171">Set the constants including **TWITTERAPPACCESSTOKEN**, **TWITTERAPPACCESSTOKENSECRET**, **TWITTERAPPAPIKEY** and **TWITTERAPPAPISECRET**.</span></span>

<span data-ttu-id="da23a-172">To run the streaming service, press **F5**.</span><span class="sxs-lookup"><span data-stu-id="da23a-172">To run the streaming service, press **F5**.</span></span> <span data-ttu-id="da23a-173">The following is a screenshot of the console application:</span><span class="sxs-lookup"><span data-stu-id="da23a-173">The following is a screenshot of the console application:</span></span>

![hdinsight.hbase.twitter.sentiment.streaming.service][img-streaming-service]

<span data-ttu-id="da23a-175">Keep the streaming console application running while you develop the web application, so you have more data to use.</span><span class="sxs-lookup"><span data-stu-id="da23a-175">Keep the streaming console application running while you develop the web application, so you have more data to use.</span></span> <span data-ttu-id="da23a-176">To examine the data inserted into the table, you can use HBase Shell.</span><span class="sxs-lookup"><span data-stu-id="da23a-176">To examine the data inserted into the table, you can use HBase Shell.</span></span> <span data-ttu-id="da23a-177">See [Get started with HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md#create-tables-and-insert-data).</span><span class="sxs-lookup"><span data-stu-id="da23a-177">See [Get started with HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md#create-tables-and-insert-data).</span></span>

## <a name="visualize-real-time-sentiment"></a><span data-ttu-id="da23a-178">Visualize real-time sentiment</span><span class="sxs-lookup"><span data-stu-id="da23a-178">Visualize real-time sentiment</span></span>
<span data-ttu-id="da23a-179">In this section, you will create an ASP.NET MVC web application to read the real-time sentiment data from HBase and plot the data on Bing maps.</span><span class="sxs-lookup"><span data-stu-id="da23a-179">In this section, you will create an ASP.NET MVC web application to read the real-time sentiment data from HBase and plot the data on Bing maps.</span></span>

<span data-ttu-id="da23a-180">**To create an ASP.NET MVC Web application**</span><span class="sxs-lookup"><span data-stu-id="da23a-180">**To create an ASP.NET MVC Web application**</span></span>

1. <span data-ttu-id="da23a-181">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da23a-181">Open Visual Studio.</span></span>
2. <span data-ttu-id="da23a-182">Click **File**, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="da23a-182">Click **File**, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="da23a-183">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="da23a-183">Enter the following information:</span></span>

   * <span data-ttu-id="da23a-184">Template category: **Visual C#/Web**</span><span class="sxs-lookup"><span data-stu-id="da23a-184">Template category: **Visual C#/Web**</span></span>
   * <span data-ttu-id="da23a-185">Template: **ASP.NET Web Application**</span><span class="sxs-lookup"><span data-stu-id="da23a-185">Template: **ASP.NET Web Application**</span></span>
   * <span data-ttu-id="da23a-186">Name: **TweetSentimentWeb**</span><span class="sxs-lookup"><span data-stu-id="da23a-186">Name: **TweetSentimentWeb**</span></span>
   * <span data-ttu-id="da23a-187">Location: **C:\Tutorials**</span><span class="sxs-lookup"><span data-stu-id="da23a-187">Location: **C:\Tutorials**</span></span>
4. <span data-ttu-id="da23a-188">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="da23a-188">Click **OK**.</span></span>
5. <span data-ttu-id="da23a-189">In **Select a template**, click **MVC**.</span><span class="sxs-lookup"><span data-stu-id="da23a-189">In **Select a template**, click **MVC**.</span></span>
6. <span data-ttu-id="da23a-190">In **Microsoft Azure**, click **Manage Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="da23a-190">In **Microsoft Azure**, click **Manage Subscriptions**.</span></span>
7. <span data-ttu-id="da23a-191">From **Manage Microsoft Azure Subscriptions**, click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="da23a-191">From **Manage Microsoft Azure Subscriptions**, click **Sign in**.</span></span>
8. <span data-ttu-id="da23a-192">Enter your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="da23a-192">Enter your Azure credentials.</span></span> <span data-ttu-id="da23a-193">Your Azure subscription information will be shown on the **Accounts** tab.</span><span class="sxs-lookup"><span data-stu-id="da23a-193">Your Azure subscription information will be shown on the **Accounts** tab.</span></span>
9. <span data-ttu-id="da23a-194">Click **Close** to close the **Manage Microsoft Azure Subscriptions** window.</span><span class="sxs-lookup"><span data-stu-id="da23a-194">Click **Close** to close the **Manage Microsoft Azure Subscriptions** window.</span></span>
10. <span data-ttu-id="da23a-195">From **New ASP.NET Project - TweetSentimentWeb**, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="da23a-195">From **New ASP.NET Project - TweetSentimentWeb**, click **OK**.</span></span>
11. <span data-ttu-id="da23a-196">From **Configure Microsoft Azure Site Settings**, select the **Region** that is closest to you.</span><span class="sxs-lookup"><span data-stu-id="da23a-196">From **Configure Microsoft Azure Site Settings**, select the **Region** that is closest to you.</span></span> <span data-ttu-id="da23a-197">You don't need to specify a database server.</span><span class="sxs-lookup"><span data-stu-id="da23a-197">You don't need to specify a database server.</span></span>
12. <span data-ttu-id="da23a-198">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="da23a-198">Click **OK**.</span></span>

<span data-ttu-id="da23a-199">**To install NuGet packages**</span><span class="sxs-lookup"><span data-stu-id="da23a-199">**To install NuGet packages**</span></span>

1. <span data-ttu-id="da23a-200">From the **Tools** menu, click **Nuget Package Manager**, and then click **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="da23a-200">From the **Tools** menu, click **Nuget Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="da23a-201">The console panel is opened at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="da23a-201">The console panel is opened at the bottom of the page.</span></span>
2. <span data-ttu-id="da23a-202">Use the following command to install the [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) package, which is the client library to access HBase cluster:</span><span class="sxs-lookup"><span data-stu-id="da23a-202">Use the following command to install the [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) package, which is the client library to access HBase cluster:</span></span>

        Install-Package Microsoft.HBase.Client

<span data-ttu-id="da23a-203">**To add HBaseReader class**</span><span class="sxs-lookup"><span data-stu-id="da23a-203">**To add HBaseReader class**</span></span>

1. <span data-ttu-id="da23a-204">From **Solution Explorer**, expand **TweetSentiment**.</span><span class="sxs-lookup"><span data-stu-id="da23a-204">From **Solution Explorer**, expand **TweetSentiment**.</span></span>
2. <span data-ttu-id="da23a-205">Right-click **Models**, click **Add**, and then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="da23a-205">Right-click **Models**, click **Add**, and then click **Class**.</span></span>
3. <span data-ttu-id="da23a-206">In the **Name** field, type **HBaseReader.cs**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="da23a-206">In the **Name** field, type **HBaseReader.cs**, and then click **Add**.</span></span>
4. <span data-ttu-id="da23a-207">Replace the code with the following:</span><span class="sxs-lookup"><span data-stu-id="da23a-207">Replace the code with the following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Web;

        using System.Configuration;
        using System.Threading.Tasks;
        using System.Text;
        using Microsoft.HBase.Client;
        using org.apache.hadoop.hbase.rest.protobuf.generated;

        namespace TweetSentimentWeb.Models
        {
            public class HBaseReader
            {
                // For reading Tweet sentiment data from HDInsight HBase
                HBaseClient client;

                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "<HBaseClusterName>";
                const string HADOOPUSERNAME = "<HBaseClusterHadoopUserName>"
                const string HADOOPUSERPASSWORD = "<HBaseCluserUserPassword>";
                const string HBASETABLENAME = "tweets_by_words";

                // The constructor
                public HBaseReader()
                {
                    ClusterCredentials creds = new ClusterCredentials(
                                    new Uri(CLUSTERNAME),
                                    HADOOPUSERNAME,
                                    HADOOPUSERPASSWORD);
                    client = new HBaseClient(creds);
                }

                // Query Tweets sentiment data from the HBase table asynchronously
                public async Task<IEnumerable<Tweet>> QueryTweetsByKeywordAsync(string keyword)
                {
                    List<Tweet> list = new List<Tweet>();

                    // Demonstrate Filtering the data from the past 6 hours the row key
                    string timeIndex = (ulong.MaxValue -
                        (ulong)DateTime.UtcNow.Subtract(new TimeSpan(6, 0, 0)).ToBinary()).ToString().PadLeft(20);
                    string startRow = keyword + "_" + timeIndex;
                    string endRow = keyword + "|";
                    Scanner scanSettings = new Scanner
                    {
                        batch = 100000,
                        startRow = Encoding.UTF8.GetBytes(startRow),
                        endRow = Encoding.UTF8.GetBytes(endRow)
                    };

                    // Make async scan call
                    ScannerInformation scannerInfo =
                        await client.CreateScannerAsync(HBASETABLENAME, scanSettings);

                    CellSet next;

                    while ((next = await client.ScannerGetNextAsync(scannerInfo)) != null)
                    {
                        foreach (CellSet.Row row in next.rows)
                        {
                            // find the cell with string pattern "d:coor"
                            var coordinates =
                                row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:coor");

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');

                                var sentimentField =
                                    row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:sentiment");
                                Int32 sentiment = 0;
                                if (sentimentField != null)
                                {
                                    sentiment = Convert.ToInt32(Encoding.UTF8.GetString(sentimentField.data));
                                }

                                list.Add(new Tweet
                                {
                                    Longtitude = Convert.ToDouble(lonlat[0]),
                                    Latitude = Convert.ToDouble(lonlat[1]),
                                    Sentiment = sentiment
                                });
                            }

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');
                            }
                        }
                    }

                    return list;
                }
            }

            public class Tweet
            {
                public string IdStr { get; set; }
                public string Text { get; set; }
                public string Lang { get; set; }
                public double Longtitude { get; set; }
                public double Latitude { get; set; }
                public int Sentiment { get; set; }
            }
        }
5. <span data-ttu-id="da23a-208">Inside the **HBaseReader** class, change the constant values as follows:</span><span class="sxs-lookup"><span data-stu-id="da23a-208">Inside the **HBaseReader** class, change the constant values as follows:</span></span>

   * <span data-ttu-id="da23a-209">**CLUSTERNAME**: The HBase cluster name, for example, *https://<HBaseClusterName>.azurehdinsight.net/*.</span><span class="sxs-lookup"><span data-stu-id="da23a-209">**CLUSTERNAME**: The HBase cluster name, for example, *https://<HBaseClusterName>.azurehdinsight.net/*.</span></span>
   * <span data-ttu-id="da23a-210">**HADOOPUSERNAME**: The HBase cluster Hadoop user user name.</span><span class="sxs-lookup"><span data-stu-id="da23a-210">**HADOOPUSERNAME**: The HBase cluster Hadoop user user name.</span></span> <span data-ttu-id="da23a-211">The default name is *admin*.</span><span class="sxs-lookup"><span data-stu-id="da23a-211">The default name is *admin*.</span></span>
   * <span data-ttu-id="da23a-212">**HADOOPUSERPASSWORD**: The HBase cluster Hadoop user password.</span><span class="sxs-lookup"><span data-stu-id="da23a-212">**HADOOPUSERPASSWORD**: The HBase cluster Hadoop user password.</span></span>
   * <span data-ttu-id="da23a-213">**HBASETABLENAME** = "tweets_by_words";</span><span class="sxs-lookup"><span data-stu-id="da23a-213">**HBASETABLENAME** = "tweets_by_words";</span></span>

     <span data-ttu-id="da23a-214">The HBase table name is **"tweets_by_words";**.</span><span class="sxs-lookup"><span data-stu-id="da23a-214">The HBase table name is **"tweets_by_words";**.</span></span> <span data-ttu-id="da23a-215">The values must match the values you sent in the streaming service, so that the web application reads the data from the same HBase table.</span><span class="sxs-lookup"><span data-stu-id="da23a-215">The values must match the values you sent in the streaming service, so that the web application reads the data from the same HBase table.</span></span>

<span data-ttu-id="da23a-216">**To add TweetsController controller**</span><span class="sxs-lookup"><span data-stu-id="da23a-216">**To add TweetsController controller**</span></span>

1. <span data-ttu-id="da23a-217">From **Solution Explorer**, expand **TweetSentimentWeb**.</span><span class="sxs-lookup"><span data-stu-id="da23a-217">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="da23a-218">Right-click **Controllers**, click **Add**, and then click **Controller**.</span><span class="sxs-lookup"><span data-stu-id="da23a-218">Right-click **Controllers**, click **Add**, and then click **Controller**.</span></span>
3. <span data-ttu-id="da23a-219">Click **Web API 2 Controller - Empty**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="da23a-219">Click **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
4. <span data-ttu-id="da23a-220">In the **Controller name** field, type **TweetsController**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="da23a-220">In the **Controller name** field, type **TweetsController**, and then click **Add**.</span></span>
5. <span data-ttu-id="da23a-221">From **Solution Explorer**, double-click TweetsController.cs to open the file.</span><span class="sxs-lookup"><span data-stu-id="da23a-221">From **Solution Explorer**, double-click TweetsController.cs to open the file.</span></span>
6. <span data-ttu-id="da23a-222">Modify the file, so it looks like the following:</span><span class="sxs-lookup"><span data-stu-id="da23a-222">Modify the file, so it looks like the following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Http;

        using System.Threading.Tasks;
        using TweetSentimentWeb.Models;

        namespace TweetSentimentWeb.Controllers
        {
            public class TweetsController : ApiController
            {
                HBaseReader hbase = new HBaseReader();

                public async Task<IEnumerable<Tweet>> GetTweetsByQuery(string query)
                {
                    return await hbase.QueryTweetsByKeywordAsync(query);
                }
            }
        }

<span data-ttu-id="da23a-223">**To add heatmap.js**</span><span class="sxs-lookup"><span data-stu-id="da23a-223">**To add heatmap.js**</span></span>

1. <span data-ttu-id="da23a-224">From **Solution Explorer**, expand **TweetSentimentWeb**.</span><span class="sxs-lookup"><span data-stu-id="da23a-224">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="da23a-225">Right-click **Scripts**, click **Add**, click **JavaScript File**.</span><span class="sxs-lookup"><span data-stu-id="da23a-225">Right-click **Scripts**, click **Add**, click **JavaScript File**.</span></span>
3. <span data-ttu-id="da23a-226">In the **Item name** field, type **heatmap.js**.</span><span class="sxs-lookup"><span data-stu-id="da23a-226">In the **Item name** field, type **heatmap.js**.</span></span>
4. <span data-ttu-id="da23a-227">Paste the following code into the file.</span><span class="sxs-lookup"><span data-stu-id="da23a-227">Paste the following code into the file.</span></span> <span data-ttu-id="da23a-228">The code was written by Alastair Aitchison.</span><span class="sxs-lookup"><span data-stu-id="da23a-228">The code was written by Alastair Aitchison.</span></span> <span data-ttu-id="da23a-229">For more information, see [Bing Maps AJAX v7 HeatMap Library](http://alastaira.wordpress.com/2011/04/15/bing-maps-ajax-v7-heatmap-library/).</span><span class="sxs-lookup"><span data-stu-id="da23a-229">For more information, see [Bing Maps AJAX v7 HeatMap Library](http://alastaira.wordpress.com/2011/04/15/bing-maps-ajax-v7-heatmap-library/).</span></span>

        /*******************************************************************************
        * Author: Alastair Aitchison
        * Website: http://alastaira.wordpress.com
        * Date: 15th April 2011
        *
        * Description:
        * This JavaScript file provides an algorithm that can be used to add a heatmap
        * overlay on a Bing Maps v7 control. The intensity and temperature palette
        * of the heatmap are designed to be easily customisable.
        *
        * Requirements:
        * The heatmap layer itself is created dynamically on the client-side using
        * the HTML5 &lt;canvas> element, and therefore requires a browser that supports
        * this element. It has been tested on IE9, Firefox 3.6/4 and
        * Chrome 10 browsers. If you can confirm whether it works on other browsers or
        * not, I'd love to hear from you!
        *
        * Usage:
        * The HeatMapLayer constructor requires:
        * - A reference to a map object
        * - An array or Microsoft.Maps.Location items
        * - Optional parameters to customise the appearance of the layer
        *  (Radius,, Unit, Intensity, and ColourGradient), and a callback function
        */

        var HeatMapLayer = function (map, locations, options) {

            /* Private Properties */
            var _map = map,
                _canvas,
                _temperaturemap,
                _locations = [],
                _viewchangestarthandler,
                _viewchangeendhandler;

            // Set default options
            var _options = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 1000,

                // Whether the radius is an absolute pixel value or meters
                unit: 'meters',

                // Colour temperature gradient of the map
                colourgradient: {
                    "0.00": 'rgba(255,0,255,20)',  // Magenta
                    "0.25": 'rgba(0,0,255,40)',    // Blue
                    "0.50": 'rgba(0,255,0,80)',    // Green
                    "0.75": 'rgba(255,255,0,120)', // Yellow
                    "1.00": 'rgba(255,0,0,150)'    // Red
                },

                // Callback function to be fired after heatmap layer has been redrawn
                callback: null
            };

            /* Private Methods */
            function _init() {
                var _mapDiv = _map.getRootElement();

                if (_mapDiv.childNodes.length >= 3 && _mapDiv.childNodes[2].childNodes.length >= 2) {
                    // Create the canvas element
                    _canvas = document.createElement('canvas');
                    _canvas.style.position = 'relative';

                    var container = document.createElement('div');
                    container.style.position = 'absolute';
                    container.style.left = '0px';
                    container.style.top = '0px';
                    container.appendChild(_canvas);

                    _mapDiv.childNodes[2].childNodes[1].appendChild(container);

                    // Override defaults with any options passed in the constructor
                    _setOptions(options);

                    // Load array of location data
                    _setPoints(locations);

                    // Create a colour gradient from the suppied colourstops
                    _temperaturemap = _createColourGradient(_options.colourgradient);

                    // Wire up the event handler to redraw heatmap canvas
                    _viewchangestarthandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangestart', _clearHeatMap);
                    _viewchangeendhandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangeend', _createHeatMap);

                    _createHeatMap();

                    delete _init;
                } else {
                    setTimeout(_init, 100);
                }
            }

            // Resets the heat map
            function _clearHeatMap() {
                var ctx = _canvas.getContext("2d");
                ctx.clearRect(0, 0, _canvas.width, _canvas.height);
            }

            // Creates a colour gradient from supplied colour stops on initialisation
            function _createColourGradient(colourstops) {
                var ctx = document.createElement('canvas').getContext('2d');
                var grd = ctx.createLinearGradient(0, 0, 256, 0);
                for (var c in colourstops) {
                    grd.addColorStop(c, colourstops[c]);
                }
                ctx.fillStyle = grd;
                ctx.fillRect(0, 0, 256, 1);
                return ctx.getImageData(0, 0, 256, 1).data;
            }

            // Applies a colour gradient to the intensity map
            function _colouriseHeatMap() {
                var ctx = _canvas.getContext("2d");
                var dat = ctx.getImageData(0, 0, _canvas.width, _canvas.height);
                var pix = dat.data; // pix is a CanvasPixelArray containing height x width x 4 bytes of data (RGBA)
                for (var p = 0, len = pix.length; p < len;) {
                    var a = pix[p + 3] * 4; // get the alpha of this pixel
                    if (a != 0) { // If there is any data to plot
                        pix[p] = _temperaturemap[a]; // set the red value of the gradient that corresponds to this alpha
                        pix[p + 1] = _temperaturemap[a + 1]; //set the green value based on alpha
                        pix[p + 2] = _temperaturemap[a + 2]; //set the blue value based on alpha
                    }
                    p += 4; // Move on to the next pixel
                }
                ctx.putImageData(dat, 0, 0);
            }

            // Sets any options passed in
            function _setOptions(options) {
                for (attrname in options) {
                    _options[attrname] = options[attrname];
                }
            }

            // Sets the heatmap points from an array of Microsoft.Maps.Locations  
            function _setPoints(locations) {
                _locations = locations;
            }

            // Main method to draw the heatmap
            function _createHeatMap() {
                // Ensure the canvas matches the current dimensions of the map
                // This also has the effect of resetting the canvas
                _canvas.height = _map.getHeight();
                _canvas.width = _map.getWidth();

                _canvas.style.top = -_canvas.height / 2 + 'px';
                _canvas.style.left = -_canvas.width / 2 + 'px';

                // Calculate the pixel radius of each heatpoint at the current map zoom
                if (_options.unit == "pixels") {
                    radiusInPixel = _options.radius;
                } else {
                    radiusInPixel = _options.radius / _map.getMetersPerPixel();
                }

                var ctx = _canvas.getContext("2d");

                // Convert lat/long to pixel location
                var pixlocs = _map.tryLocationToPixel(_locations, Microsoft.Maps.PixelReference.control);
                var shadow = 'rgba(0, 0, 0, ' + _options.intensity + ')';
                var mapWidth = 256 * Math.pow(2, _map.getZoom());

                // Create the Intensity Map by looping through each location
                for (var i = 0, len = pixlocs.length; i < len; i++) {
                    var x = pixlocs[i].x;
                    var y = pixlocs[i].y;

                    if (x < 0) {
                        x += mapWidth * Math.ceil(Math.abs(x / mapWidth));
                    }

                    // Create radial gradient centred on this point
                    var grd = ctx.createRadialGradient(x, y, 0, x, y, radiusInPixel);
                    grd.addColorStop(0.0, shadow);
                    grd.addColorStop(1.0, 'transparent');

                    // Draw the heatpoint onto the canvas
                    ctx.fillStyle = grd;
                    ctx.fillRect(x - radiusInPixel, y - radiusInPixel, 2 * radiusInPixel, 2 * radiusInPixel);
                }

                // Apply the specified colour gradient to the intensity map
                _colouriseHeatMap();

                // Call the callback function, if specified
                if (_options.callback) {
                    _options.callback();
                }
            }

            /* Public Methods */

            this.Show = function () {
                if (_canvas) {
                    _canvas.style.display = '';
                }
            };

            this.Hide = function () {
                if (_canvas) {
                    _canvas.style.display = 'none';
                }
            };

            // Sets options for intensity, radius, colourgradient etc.
            this.SetOptions = function (options) {
                _setOptions(options);
            }

            // Sets an array of Microsoft.Maps.Locations from which the heatmap is created
            this.SetPoints = function (locations) {
                // Reset the existing heatmap layer
                _clearHeatMap();
                // Pass in the new set of locations
                _setPoints(locations);
                // Recreate the layer
                _createHeatMap();
            }

            // Removes the heatmap layer from the DOM
            this.Remove = function () {
                _canvas.parentNode.parentNode.removeChild(_canvas.parentNode);

                if (_viewchangestarthandler) { Microsoft.Maps.Events.removeHandler(_viewchangestarthandler); }
                if (_viewchangeendhandler) { Microsoft.Maps.Events.removeHandler(_viewchangeendhandler); }

                _locations = null;
                _temperaturemap = null;
                _canvas = null;
                _options = null;
                _viewchangestarthandler = null;
                _viewchangeendhandler = null;
            }

            // Call the initialisation routine
            _init();
        };

        // Call the Module Loaded method
        Microsoft.Maps.moduleLoaded('HeatMapModule');

<span data-ttu-id="da23a-230">**To add twitterStream.js**</span><span class="sxs-lookup"><span data-stu-id="da23a-230">**To add twitterStream.js**</span></span>

1. <span data-ttu-id="da23a-231">From **Solution Explorer**, expand **TweetSentimentWeb**.</span><span class="sxs-lookup"><span data-stu-id="da23a-231">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="da23a-232">Right-click **Scripts**, click **Add**, click **JavaScript File**.</span><span class="sxs-lookup"><span data-stu-id="da23a-232">Right-click **Scripts**, click **Add**, click **JavaScript File**.</span></span>
3. <span data-ttu-id="da23a-233">In the **Item name** field, type**twitterStream.js**.</span><span class="sxs-lookup"><span data-stu-id="da23a-233">In the **Item name** field, type**twitterStream.js**.</span></span>
4. <span data-ttu-id="da23a-234">Copy and paste the following code into the file:</span><span class="sxs-lookup"><span data-stu-id="da23a-234">Copy and paste the following code into the file:</span></span>

        var liveTweetsPos = [];
        var liveTweets = [];
        var liveTweetsNeg = [];
        var map;
        var heatmap;
        var heatmapNeg;
        var heatmapPos;

        function initialize() {
            // Initialize the map
            var options = {
                credentials: "AvFJTZPZv8l3gF8VC3Y7BPBd0r7LKo8dqKG02EAlqg9WAi0M7la6zSIT-HwkMQbx",
                center: new Microsoft.Maps.Location(23.0, 8.0),
                mapTypeId: Microsoft.Maps.MapTypeId.ordnanceSurvey,
                labelOverlay: Microsoft.Maps.LabelOverlay.hidden,
                zoom: 2.5
            };
            var map = new Microsoft.Maps.Map(document.getElementById('map_canvas'), options);

            // Heatmap options for positive, neutral and negative layers

            var heatmapOptions = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether the radius is an absolute pixel value or meters
                unit: 'pixels'
            };

            var heatmapPosOptions = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether the radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 255, 191, 1)',
                    0.3: 'rgba(0, 255, 127, 1)',
                    0.4: 'rgba(0, 255, 63, 1)',
                    0.5: 'rgba(0, 127, 0, 1)',
                    0.7: 'rgba(0, 159, 0, 1)',
                    0.8: 'rgba(0, 191, 0, 1)',
                    0.9: 'rgba(0, 223, 0, 1)',
                    1.0: 'rgba(0, 255, 0, 1)'
                }
            };

            var heatmapNegOptions = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether the radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 191, 255, 1)',
                    0.3: 'rgba(0, 127, 255, 1)',
                    0.4: 'rgba(0, 63, 255, 1)',
                    0.5: 'rgba(0, 0, 127, 1)',
                    0.7: 'rgba(0, 0, 159, 1)',
                    0.8: 'rgba(0, 0, 191, 1)',
                    0.9: 'rgba(0, 0, 223, 1)',
                    1.0: 'rgba(0, 0, 255, 1)'
                }
            };

            // Register and load the Client Side HeatMap Module
            Microsoft.Maps.registerModule("HeatMapModule", "scripts/heatmap.js");
            Microsoft.Maps.loadModule("HeatMapModule", {
                callback: function () {
                    // Create heatmap layers for positive, neutral and negative tweets
                    heatmapPos = new HeatMapLayer(map, liveTweetsPos, heatmapPosOptions);
                    heatmap = new HeatMapLayer(map, liveTweets, heatmapOptions);
                    heatmapNeg = new HeatMapLayer(map, liveTweetsNeg, heatmapNegOptions);
                }
            });

            $("#searchbox").val("xbox");
            $("#searchBtn").click(onsearch);
            $("#positiveBtn").click(onPositiveBtn);
            $("#negativeBtn").click(onNegativeBtn);
            $("#neutralBtn").click(onNeutralBtn);
            $("#neutralBtn").button("toggle");
        }

        function onsearch() {
            var uri = 'api/tweets?query=';
            var query = $('#searchbox').val();
            $.getJSON(uri + query)
                .done(function (data) {
                    liveTweetsPos = [];
                    liveTweets = [];
                    liveTweetsNeg = [];

                    // On success, 'data' contains a list of tweets.
                    $.each(data, function (key, item) {
                        addTweet(item);
                    });

                    if (!$("#neutralBtn").hasClass('active')) {
                        $("#neutralBtn").button("toggle");
                    }
                    onNeutralBtn();
                })
                .fail(function (jqXHR, textStatus, err) {
                    $('#statustext').text('Error: ' + err);
                });
        }

        function addTweet(item) {
            //Add tweet to the heat map arrays.
            var tweetLocation = new Microsoft.Maps.Location(item.Latitude, item.Longtitude);
            if (item.Sentiment > 0) {
                liveTweetsPos.push(tweetLocation);
            } else if (item.Sentiment < 0) {
                liveTweetsNeg.push(tweetLocation);
            } else {
                liveTweets.push(tweetLocation);
            }
        }

        function onPositiveBtn() {
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmapPos.SetPoints(liveTweetsPos);
            heatmapPos.Show();
            heatmapNeg.Hide();
            heatmap.Hide();

            $('#statustext').text('Tweets: ' + liveTweetsPos.length + "   " + getPosNegRatio());
        }

        function onNeutralBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmap.SetPoints(liveTweets);
            heatmap.Show();
            heatmapNeg.Hide();
            heatmapPos.Hide();

            $('#statustext').text('Tweets: ' + liveTweets.length + "   " + getPosNegRatio());
        }

        function onNegativeBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }

            heatmapNeg.SetPoints(liveTweetsNeg);
            heatmapNeg.Show();
            heatmap.Hide();;
            heatmapPos.Hide();;

            $('#statustext').text('Tweets: ' + liveTweetsNeg.length + "\t" + getPosNegRatio());
        }

        function getPosNegRatio() {
            if (liveTweetsNeg.length == 0) {
                return "";
            }
            else {
                var ratio = liveTweetsPos.length / liveTweetsNeg.length;
                var str = parseFloat(Math.round(ratio * 10) / 10).toFixed(1);
                return "Positive/Negative Ratio: " + str;
            }
        }

<span data-ttu-id="da23a-235">**To modify the layout.cshtml**</span><span class="sxs-lookup"><span data-stu-id="da23a-235">**To modify the layout.cshtml**</span></span>

1. <span data-ttu-id="da23a-236">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Views**, expand **Shared**, and then double-click _**Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="da23a-236">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Views**, expand **Shared**, and then double-click _**Layout.cshtml**.</span></span>
2. <span data-ttu-id="da23a-237">Replace the content with the following:</span><span class="sxs-lookup"><span data-stu-id="da23a-237">Replace the content with the following:</span></span>

        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="utf-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>@ViewBag.Title</title>
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
            <!-- Bing Maps -->
            <script type="text/javascript" src="http://ecn.dev.virtualearth.net/mapcontrol/mapcontrol.ashx?v=7.0&mkt=en-gb"></script>
            <!-- Spatial Dashboard JavaScript -->
            <script src="~/Scripts/twitterStream.js" type="text/javascript"></script>
        </head>
        <body onload="initialize()">
            <div class="navbar navbar-inverse navbar-fixed-top">
                <div class="container">
                    <div class="navbar-header">
                        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                        </button>
                    </div>
                    <div class="navbar-collapse collapse">
                        <div class="row">
                            <ul class="nav navbar-nav col-lg-5">
                                <li class="col-lg-12">
                                    <div class="navbar-form">
                                        <input id="searchbox" type="search" class="form-control">
                                        <button type="button" id="searchBtn" class="btn btn-primary">Go</button>
                                    </div>
                                </li>
                            </ul>
                            <ul class="nav navbar-nav col-lg-7">
                                <li>
                                    <div class="navbar-form">
                                        <div class="btn-group" data-toggle="buttons-radio">
                                            <button type="button" id="positiveBtn" class="btn btn-primary">Positive</button>
                                            <button type="button" id="neutralBtn" class="btn btn-primary">Neutral</button>
                                            <button type="button" id="negativeBtn" class="btn btn-primary">Negative</button>
                                        </div>
                                    </div>
                                </li>
                                <li><span id="statustext" class="navbar-text"></span></li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
            <div class="map_container">
                @RenderBody()
            </div>
            @Scripts.Render("~/bundles/jquery")
            @Scripts.Render("~/bundles/bootstrap")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="da23a-238">**To modify the Index.cshtml**</span><span class="sxs-lookup"><span data-stu-id="da23a-238">**To modify the Index.cshtml**</span></span>

1. <span data-ttu-id="da23a-239">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Views**, expand **Home**, and then double-click **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="da23a-239">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Views**, expand **Home**, and then double-click **Index.cshtml**.</span></span>
2. <span data-ttu-id="da23a-240">Replace the content with the following:</span><span class="sxs-lookup"><span data-stu-id="da23a-240">Replace the content with the following:</span></span>

        @{
            ViewBag.Title = "Tweet Sentiment";
        }

        <div class="map_container">
            <div id="map_canvas"/>
        </div>

<span data-ttu-id="da23a-241">**To modify the site.css file**</span><span class="sxs-lookup"><span data-stu-id="da23a-241">**To modify the site.css file**</span></span>

1. <span data-ttu-id="da23a-242">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Content**, and then double-click **Site.css**.</span><span class="sxs-lookup"><span data-stu-id="da23a-242">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Content**, and then double-click **Site.css**.</span></span>
2. <span data-ttu-id="da23a-243">Append the following code to the file:</span><span class="sxs-lookup"><span data-stu-id="da23a-243">Append the following code to the file:</span></span>

        /* make container, and thus map, 100% width */
        .map_container {
            width: 100%;
            height: 100%;
        }

        #map_canvas{
          height:100%;
        }

        #tweets{
          position: absolute;
          top: 60px;
          left: 75px;
          z-index:1000;
          font-size: 30px;
        }

<span data-ttu-id="da23a-244">**To modify the global.asax file**</span><span class="sxs-lookup"><span data-stu-id="da23a-244">**To modify the global.asax file**</span></span>

1. <span data-ttu-id="da23a-245">From **Solution Explorer**, expand **TweetSentimentWeb**, and then double-click **Global.asax**.</span><span class="sxs-lookup"><span data-stu-id="da23a-245">From **Solution Explorer**, expand **TweetSentimentWeb**, and then double-click **Global.asax**.</span></span>
2. <span data-ttu-id="da23a-246">Add the following **using** statement:</span><span class="sxs-lookup"><span data-stu-id="da23a-246">Add the following **using** statement:</span></span>

        using System.Web.Http;
3. <span data-ttu-id="da23a-247">Add the following lines inside the **Application_Start()** function:</span><span class="sxs-lookup"><span data-stu-id="da23a-247">Add the following lines inside the **Application_Start()** function:</span></span>

        // Register API routes
        GlobalConfiguration.Configure(WebApiConfig.Register);

    <span data-ttu-id="da23a-248">Modify the registration of the API routes to make the Web API controller work inside the MVC application.</span><span class="sxs-lookup"><span data-stu-id="da23a-248">Modify the registration of the API routes to make the Web API controller work inside the MVC application.</span></span>

<span data-ttu-id="da23a-249">**To run the web application**</span><span class="sxs-lookup"><span data-stu-id="da23a-249">**To run the web application**</span></span>

1. <span data-ttu-id="da23a-250">Verify that the streaming service console application is still running so you can see the real-time changes.</span><span class="sxs-lookup"><span data-stu-id="da23a-250">Verify that the streaming service console application is still running so you can see the real-time changes.</span></span>
2. <span data-ttu-id="da23a-251">Press **F5** to run the web application:</span><span class="sxs-lookup"><span data-stu-id="da23a-251">Press **F5** to run the web application:</span></span>

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]
3. <span data-ttu-id="da23a-253">In the text box, enter a keyword, and then click **Go**.</span><span class="sxs-lookup"><span data-stu-id="da23a-253">In the text box, enter a keyword, and then click **Go**.</span></span>  <span data-ttu-id="da23a-254">Depending on the data collected in the HBase table, some keywords might not be found.</span><span class="sxs-lookup"><span data-stu-id="da23a-254">Depending on the data collected in the HBase table, some keywords might not be found.</span></span> <span data-ttu-id="da23a-255">Try some common keywords, such as "love," "xbox," and "playstation."</span><span class="sxs-lookup"><span data-stu-id="da23a-255">Try some common keywords, such as "love," "xbox," and "playstation."</span></span>
4. <span data-ttu-id="da23a-256">Toggle among **Positive**, **Neutral**, and **Negative** to compare sentiment on the subject.</span><span class="sxs-lookup"><span data-stu-id="da23a-256">Toggle among **Positive**, **Neutral**, and **Negative** to compare sentiment on the subject.</span></span>
5. <span data-ttu-id="da23a-257">Let the streaming service run for another hour, and then search the same keywords, and compare the results.</span><span class="sxs-lookup"><span data-stu-id="da23a-257">Let the streaming service run for another hour, and then search the same keywords, and compare the results.</span></span>

<span data-ttu-id="da23a-258">Optionally, you can deploy the application to Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="da23a-258">Optionally, you can deploy the application to Azure Websites.</span></span> <span data-ttu-id="da23a-259">For instructions, see [Get started with Azure Websites and ASP.NET][website-get-started].</span><span class="sxs-lookup"><span data-stu-id="da23a-259">For instructions, see [Get started with Azure Websites and ASP.NET][website-get-started].</span></span>

## <a name="next-steps"></a><span data-ttu-id="da23a-260">Next Steps</span><span class="sxs-lookup"><span data-stu-id="da23a-260">Next Steps</span></span>
<span data-ttu-id="da23a-261">In this tutorial, you learned how to get tweets, analyze the sentiment of tweets, save the sentiment data to HBase, and present the real-time Twitter sentiment data to Bing maps.</span><span class="sxs-lookup"><span data-stu-id="da23a-261">In this tutorial, you learned how to get tweets, analyze the sentiment of tweets, save the sentiment data to HBase, and present the real-time Twitter sentiment data to Bing maps.</span></span> <span data-ttu-id="da23a-262">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="da23a-262">To learn more, see:</span></span>

* <span data-ttu-id="da23a-263">[Get started with HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="da23a-263">[Get started with HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="da23a-264">Configure HBase replication in HDInsight</span><span class="sxs-lookup"><span data-stu-id="da23a-264">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* <span data-ttu-id="da23a-265">[Analyze Twitter data with Hadoop in HDInsight][hdinsight-analyze-twitter-data]</span><span class="sxs-lookup"><span data-stu-id="da23a-265">[Analyze Twitter data with Hadoop in HDInsight][hdinsight-analyze-twitter-data]</span></span>
* <span data-ttu-id="da23a-266">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="da23a-266">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="da23a-267">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="da23a-267">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[website-get-started]: ../app-service-web/app-service-web-get-started-dotnet.md



[img-app-arch]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-analyze-twitter-sentiment/AppArchitecture.png
[img-twitter-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-analyze-twitter-sentiment/TwitterApp.png
[img-streaming-service]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-analyze-twitter-sentiment/StreamingService.png
[img-bing-map]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-analyze-twitter-sentiment/TwitterSentimentBingMap.png



[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-analyze-twitter-data]: hdinsight-analyze-twitter-data.md




[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md




