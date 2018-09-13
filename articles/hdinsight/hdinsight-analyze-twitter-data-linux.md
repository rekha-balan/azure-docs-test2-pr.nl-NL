---
title: Analyze Twitter data with Apache Hive on HDInsight | Microsoft Docs
description: Learn how to use Python to store Tweets that contain specific keywords, then use Hive and Hadoop on HDInsight to transform the raw TWitter data into a searchable Hive table.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 75368be1bb5da28df8bc29ca2d8811a822c0816e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563876"
---
# <a name="analyze-twitter-data-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="ab5a8-103">Analyze Twitter data using Hive on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab5a8-103">Analyze Twitter data using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="ab5a8-104">Learn how to use Apache Hive on an HDInsight cluster to process the Twitter data.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-104">Learn how to use Apache Hive on an HDInsight cluster to process the Twitter data.</span></span> <span data-ttu-id="ab5a8-105">The result is a list of Twitter users who sent the most tweets that contain a certain word.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-105">The result is a list of Twitter users who sent the most tweets that contain a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab5a8-106">The steps in this document were tested on a Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-106">The steps in this document were tested on a Linux-based HDInsight cluster.</span></span>
>
> <span data-ttu-id="ab5a8-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ab5a8-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="ab5a8-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab5a8-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ab5a8-109">Prerequisites</span></span>

* <span data-ttu-id="ab5a8-110">A **Linux-based Azure HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-110">A **Linux-based Azure HDInsight cluster**.</span></span> <span data-ttu-id="ab5a8-111">For information on creating a cluster, see [Get Started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a cluster.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-111">For information on creating a cluster, see [Get Started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a cluster.</span></span>
* <span data-ttu-id="ab5a8-112">An **SSH client**.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-112">An **SSH client**.</span></span> <span data-ttu-id="ab5a8-113">For more information on using SSH with Linux-based HDInsight, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-113">For more information on using SSH with Linux-based HDInsight, see the following articles:</span></span>

  * [<span data-ttu-id="ab5a8-114">Use SSH with Linux-based Hadoop on HDInsight from Linux, Unix, or OS X</span><span class="sxs-lookup"><span data-stu-id="ab5a8-114">Use SSH with Linux-based Hadoop on HDInsight from Linux, Unix, or OS X</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
  * [<span data-ttu-id="ab5a8-115">Use SSH with Linux-based Hadoop on HDInsight from Windows</span><span class="sxs-lookup"><span data-stu-id="ab5a8-115">Use SSH with Linux-based Hadoop on HDInsight from Windows</span></span>](hdinsight-hadoop-linux-use-ssh-windows.md)
* <span data-ttu-id="ab5a8-116">**Python** and [pip](https://pypi.python.org/pypi/pip)</span><span class="sxs-lookup"><span data-stu-id="ab5a8-116">**Python** and [pip](https://pypi.python.org/pypi/pip)</span></span>

## <a name="get-a-twitter-feed"></a><span data-ttu-id="ab5a8-117">Get a Twitter feed</span><span class="sxs-lookup"><span data-stu-id="ab5a8-117">Get a Twitter feed</span></span>

<span data-ttu-id="ab5a8-118">Twitter allows you to retrieve the [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-118">Twitter allows you to retrieve the [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span></span> <span data-ttu-id="ab5a8-119">[OAuth](http://oauth.net) is required for authentication to the API.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-119">[OAuth](http://oauth.net) is required for authentication to the API.</span></span>

### <a name="create-a-twitter-application"></a><span data-ttu-id="ab5a8-120">Create a Twitter application</span><span class="sxs-lookup"><span data-stu-id="ab5a8-120">Create a Twitter application</span></span>

1. <span data-ttu-id="ab5a8-121">From a web browser, sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="ab5a8-121">From a web browser, sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="ab5a8-122">Click the **Sign-up now** link if you don't have a Twitter account.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-122">Click the **Sign-up now** link if you don't have a Twitter account.</span></span>

2. <span data-ttu-id="ab5a8-123">Click **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-123">Click **Create New App**.</span></span>

3. <span data-ttu-id="ab5a8-124">Enter **Name**, **Description**, **Website**.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-124">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="ab5a8-125">You can make up a URL for the **Website** field.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-125">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="ab5a8-126">The following table shows some sample values to use:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-126">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="ab5a8-127">Field</span><span class="sxs-lookup"><span data-stu-id="ab5a8-127">Field</span></span> | <span data-ttu-id="ab5a8-128">Value</span><span class="sxs-lookup"><span data-stu-id="ab5a8-128">Value</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="ab5a8-129">Name</span><span class="sxs-lookup"><span data-stu-id="ab5a8-129">Name</span></span> |<span data-ttu-id="ab5a8-130">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="ab5a8-130">MyHDInsightApp</span></span> |
   | <span data-ttu-id="ab5a8-131">Description</span><span class="sxs-lookup"><span data-stu-id="ab5a8-131">Description</span></span> |<span data-ttu-id="ab5a8-132">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="ab5a8-132">MyHDInsightApp</span></span> |
   | <span data-ttu-id="ab5a8-133">Website</span><span class="sxs-lookup"><span data-stu-id="ab5a8-133">Website</span></span> |http://www.myhdinsightapp.com |

4. <span data-ttu-id="ab5a8-134">Check **Yes, I agree**, and then click **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-134">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>

5. <span data-ttu-id="ab5a8-135">Click the **Permissions** tab. The default permission is **Read only**.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-135">Click the **Permissions** tab. The default permission is **Read only**.</span></span>

6. <span data-ttu-id="ab5a8-136">Click the **Keys and Access Tokens** tab.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-136">Click the **Keys and Access Tokens** tab.</span></span>

7. <span data-ttu-id="ab5a8-137">Click **Create my access token**.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-137">Click **Create my access token**.</span></span>

8. <span data-ttu-id="ab5a8-138">Click **Test OAuth** in the upper-right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-138">Click **Test OAuth** in the upper-right corner of the page.</span></span>

9. <span data-ttu-id="ab5a8-139">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-139">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span>

> [!NOTE]
> <span data-ttu-id="ab5a8-140">When you use the curl command in Windows, use double quotes instead of single quotes for the option values.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-140">When you use the curl command in Windows, use double quotes instead of single quotes for the option values.</span></span>


### <a name="download-tweets"></a><span data-ttu-id="ab5a8-141">Download tweets</span><span class="sxs-lookup"><span data-stu-id="ab5a8-141">Download tweets</span></span>

<span data-ttu-id="ab5a8-142">The following Python code downloads 10,000 tweets from Twitter and save them to a file named **tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-142">The following Python code downloads 10,000 tweets from Twitter and save them to a file named **tweets.txt**.</span></span>

> [!NOTE]
> <span data-ttu-id="ab5a8-143">The following steps are performed on the HDInsight cluster, since Python is already installed.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-143">The following steps are performed on the HDInsight cluster, since Python is already installed.</span></span>
>
>

1. <span data-ttu-id="ab5a8-144">Connect to the HDInsight cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-144">Connect to the HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="ab5a8-145">If you used a password to secure your SSH user account, you are prompted to enter it.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-145">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="ab5a8-146">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-146">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="ab5a8-147">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-147">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="ab5a8-148">For more information on using SSH with Linux-based HDInsight, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-148">For more information on using SSH with Linux-based HDInsight, see the following articles:</span></span>

   * [<span data-ttu-id="ab5a8-149">Use SSH with Linux-based Hadoop on HDInsight from Linux, Unix, or OS X</span><span class="sxs-lookup"><span data-stu-id="ab5a8-149">Use SSH with Linux-based Hadoop on HDInsight from Linux, Unix, or OS X</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
   * [<span data-ttu-id="ab5a8-150">Use SSH with Linux-based Hadoop on HDInsight from Windows</span><span class="sxs-lookup"><span data-stu-id="ab5a8-150">Use SSH with Linux-based Hadoop on HDInsight from Windows</span></span>](hdinsight-hadoop-linux-use-ssh-windows.md)

2. <span data-ttu-id="ab5a8-151">By default, the **pip** utility is not installed on the HDInsight head node.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-151">By default, the **pip** utility is not installed on the HDInsight head node.</span></span> <span data-ttu-id="ab5a8-152">Use the following to install, and then update this utility:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-152">Use the following to install, and then update this utility:</span></span>

   ```bash
   sudo apt-get install python-pip
   sudo pip install --upgrade pip
   ```

3. <span data-ttu-id="ab5a8-153">Use the following commands to install [Tweepy](http://www.tweepy.org/) and [Progressbar](https://pypi.python.org/pypi/progressbar/2.2):</span><span class="sxs-lookup"><span data-stu-id="ab5a8-153">Use the following commands to install [Tweepy](http://www.tweepy.org/) and [Progressbar](https://pypi.python.org/pypi/progressbar/2.2):</span></span>

   ```bash
   sudo apt-get install python-dev libffi-dev libssl-dev
   sudo apt-get remove python-openssl
   sudo pip install tweepy progressbar pyOpenSSL requests[security]
   ```

   > [!NOTE]
   > <span data-ttu-id="ab5a8-154">The bits about removing python-openssl, installing python-dev, libffi-dev, libssl-dev, pyOpenSSL, and requests[security] is to avoid an InsecurePlatform warning when connecting to Twitter via SSL from Python.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-154">The bits about removing python-openssl, installing python-dev, libffi-dev, libssl-dev, pyOpenSSL, and requests[security] is to avoid an InsecurePlatform warning when connecting to Twitter via SSL from Python.</span></span>
   >
   > <span data-ttu-id="ab5a8-155">Tweepy v3.2.0 is used to avoid [an error](https://github.com/tweepy/tweepy/issues/576) that can occur when processing tweets.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-155">Tweepy v3.2.0 is used to avoid [an error](https://github.com/tweepy/tweepy/issues/576) that can occur when processing tweets.</span></span>

4. <span data-ttu-id="ab5a8-156">Use the following command to create a file named **gettweets.py**:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-156">Use the following command to create a file named **gettweets.py**:</span></span>

   ```bash
   nano gettweets.py
   ```

5. <span data-ttu-id="ab5a8-157">Use the following text as the contents of the **gettweets.py** file.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-157">Use the following text as the contents of the **gettweets.py** file.</span></span> <span data-ttu-id="ab5a8-158">Replace the placeholder information for **consumer\_secret**, **consumer\_key**, **access/\_token**, and **access\_token\_secret** with the information from your Twitter application.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-158">Replace the placeholder information for **consumer\_secret**, **consumer\_key**, **access/\_token**, and **access\_token\_secret** with the information from your Twitter application.</span></span>

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #The number of tweets we want to get
   max_tweets=10000

   #Create the listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set the counter to zero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append the tweet to the 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment the number of tweets
               self.num_tweets += 1
               #Check to see if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment the progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get the OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use the listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

6. <span data-ttu-id="ab5a8-159">Use **Ctrl + X**, then **Y** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-159">Use **Ctrl + X**, then **Y** to save the file.</span></span>

7. <span data-ttu-id="ab5a8-160">Use the following command to run the file and download tweets:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-160">Use the following command to run the file and download tweets:</span></span>

    ```bash
    python gettweets.py
    ```

    <span data-ttu-id="ab5a8-161">A progress indicator should appear, and count up to 100% as the tweets are downloaded and saved to file.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-161">A progress indicator should appear, and count up to 100% as the tweets are downloaded and saved to file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ab5a8-162">If it is taking a long time for the progress bar to advance, you should change the filter to track trending topics.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-162">If it is taking a long time for the progress bar to advance, you should change the filter to track trending topics.</span></span> <span data-ttu-id="ab5a8-163">When there are many tweets about the topic in your filter, you can quickly get the 10000 tweets needed.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-163">When there are many tweets about the topic in your filter, you can quickly get the 10000 tweets needed.</span></span>

### <a name="upload-the-data"></a><span data-ttu-id="ab5a8-164">Upload the data</span><span class="sxs-lookup"><span data-stu-id="ab5a8-164">Upload the data</span></span>

<span data-ttu-id="ab5a8-165">To upload the data to HDInsight storage, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-165">To upload the data to HDInsight storage, use the following commands:</span></span>

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

<span data-ttu-id="ab5a8-166">These commands store the data in a location that all nodes in the cluster can access.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-166">These commands store the data in a location that all nodes in the cluster can access.</span></span>

## <a name="run-the-hiveql-job"></a><span data-ttu-id="ab5a8-167">Run the HiveQL job</span><span class="sxs-lookup"><span data-stu-id="ab5a8-167">Run the HiveQL job</span></span>

1. <span data-ttu-id="ab5a8-168">Use the following command to create a file containing HiveQL statements:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-168">Use the following command to create a file containing HiveQL statements:</span></span>

   ```bash
   nano twitter.hql
   ```

    <span data-ttu-id="ab5a8-169">Use the following text as the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-169">Use the following text as the contents of the file:</span></span>

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward the tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate the destination table
   DROP TABLE tweets;
   CREATE TABLE tweets
   (
       id BIGINT,
       created_at STRING,
       created_at_date STRING,
       created_at_year STRING,
       created_at_month STRING,
       created_at_day STRING,
       created_at_time STRING,
       in_reply_to_user_id_str STRING,
       text STRING,
       contributors STRING,
       retweeted STRING,
       truncated STRING,
       coordinates STRING,
       source STRING,
       retweet_count INT,
       url STRING,
       hashtags array<STRING>,
       user_mentions array<STRING>,
       first_hashtag STRING,
       first_user_mention STRING,
       screen_name STRING,
       name STRING,
       followers_count INT,
       listed_count INT,
       friends_count INT,
       lang STRING,
       user_location STRING,
       time_zone STRING,
       profile_image_url STRING,
       json_response STRING
   );
   -- Select tweets from the imported data, parse the JSON,
   -- and insert into the tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
           when "Jan" then "01"
           when "Feb" then "02"
           when "Mar" then "03"
           when "Apr" then "04"
           when "May" then "05"
           when "Jun" then "06"
           when "Jul" then "07"
           when "Aug" then "08"
           when "Sep" then "09"
           when "Oct" then "10"
           when "Nov" then "11"
           when "Dec" then "12" end,
       substr (get_json_object(json_response, '$.created_at'),9,2),
       substr (get_json_object(json_response, '$.created_at'),12,8),
       get_json_object(json_response, '$.in_reply_to_user_id_str'),
       get_json_object(json_response, '$.text'),
       get_json_object(json_response, '$.contributors'),
       get_json_object(json_response, '$.retweeted'),
       get_json_object(json_response, '$.truncated'),
       get_json_object(json_response, '$.coordinates'),
       get_json_object(json_response, '$.source'),
       cast (get_json_object(json_response, '$.retweet_count') as INT),
       get_json_object(json_response, '$.entities.display_url'),
       array(
           trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
       array(
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
       trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
       trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
       get_json_object(json_response, '$.user.screen_name'),
       get_json_object(json_response, '$.user.name'),
       cast (get_json_object(json_response, '$.user.followers_count') as INT),
       cast (get_json_object(json_response, '$.user.listed_count') as INT),
       cast (get_json_object(json_response, '$.user.friends_count') as INT),
       get_json_object(json_response, '$.user.lang'),
       get_json_object(json_response, '$.user.location'),
       get_json_object(json_response, '$.user.time_zone'),
       get_json_object(json_response, '$.user.profile_image_url'),
       json_response
   WHERE (length(json_response) > 500);
   ```

2. <span data-ttu-id="ab5a8-170">Press **Ctrl + X**, then press **Y** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-170">Press **Ctrl + X**, then press **Y** to save the file.</span></span>
3. <span data-ttu-id="ab5a8-171">Use the following command to run the HiveQL contained in the file:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-171">Use the following command to run the HiveQL contained in the file:</span></span>

   ```bash
   beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin -i twitter.hql
   ```

    <span data-ttu-id="ab5a8-172">This command runs the the **twitter.hql** file.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-172">This command runs the the **twitter.hql** file.</span></span> <span data-ttu-id="ab5a8-173">Once the query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-173">Once the query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span></span>

4. <span data-ttu-id="ab5a8-174">From the beeline prompt, use the following to verify that you can select data from the **tweets** table created by the HiveQL in the **twitter.hql** file:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-174">From the beeline prompt, use the following to verify that you can select data from the **tweets** table created by the HiveQL in the **twitter.hql** file:</span></span>

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    <span data-ttu-id="ab5a8-175">This query returns a maximum of 10 tweets that contain the word **Azure** in the message text.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-175">This query returns a maximum of 10 tweets that contain the word **Azure** in the message text.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab5a8-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="ab5a8-176">Next steps</span></span>

<span data-ttu-id="ab5a8-177">You have learned how to transform an unstructured JSON dataset into a structured Hive table.</span><span class="sxs-lookup"><span data-stu-id="ab5a8-177">You have learned how to transform an unstructured JSON dataset into a structured Hive table.</span></span> <span data-ttu-id="ab5a8-178">To learn more about Hive on HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="ab5a8-178">To learn more about Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="ab5a8-179">Get started with HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab5a8-179">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="ab5a8-180">Analyze flight delay data using HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab5a8-180">Analyze flight delay data using HDInsight</span></span>](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
