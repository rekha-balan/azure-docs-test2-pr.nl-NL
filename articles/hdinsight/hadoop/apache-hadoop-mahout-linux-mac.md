---
title: Generate recommendations using Mahout and HDInsight (SSH) - Azure
description: Learn how to use the Apache Mahout machine learning library to generate movie recommendations with HDInsight (Hadoop).
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/01/2018
ms.openlocfilehash: bdf2de58db87841b4dd0dda808667baa38851d02
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867710"
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="6c2f4-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span><span class="sxs-lookup"><span data-stu-id="6c2f4-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="6c2f4-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span>

<span data-ttu-id="6c2f4-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="6c2f4-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="6c2f4-107">In this article, you use a recommendation engine to generate movie recommendations that are based on movies your friends have seen.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-107">In this article, you use a recommendation engine to generate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c2f4-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c2f4-108">Prerequisites</span></span>

* <span data-ttu-id="6c2f4-109">A Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="6c2f4-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="6c2f4-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c2f4-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6c2f4-112">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6c2f4-112">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="6c2f4-113">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-113">An SSH client.</span></span> <span data-ttu-id="6c2f4-114">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-114">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="6c2f4-115">Mahout versioning</span><span class="sxs-lookup"><span data-stu-id="6c2f4-115">Mahout versioning</span></span>

<span data-ttu-id="6c2f4-116">For more information about the version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](../hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="6c2f4-116">For more information about the version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](../hdinsight-component-versioning.md).</span></span>

## <a name="recommendations"></a><span data-ttu-id="6c2f4-117">Understanding recommendations</span><span class="sxs-lookup"><span data-stu-id="6c2f4-117">Understanding recommendations</span></span>

<span data-ttu-id="6c2f4-118">One of the functions that is provided by Mahout is a recommendation engine.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-118">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="6c2f4-119">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the preference for the item).</span><span class="sxs-lookup"><span data-stu-id="6c2f4-119">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the preference for the item).</span></span> <span data-ttu-id="6c2f4-120">Mahout can then perform co-occurrence analysis to determine: *users who have a preference for an item also have a preference for these other items*.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-120">Mahout can then perform co-occurrence analysis to determine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="6c2f4-121">Mahout then determines users with like-item preferences, which can be used to make recommendations.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-121">Mahout then determines users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="6c2f4-122">The following workflow is a simplified example that uses movie data:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-122">The following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="6c2f4-123">**Co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-123">**Co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="6c2f4-124">Mahout determines that users who like any one of these movies also like the other two.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-124">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="6c2f4-125">**Co-occurrence**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-125">**Co-occurrence**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="6c2f4-126">Mahout determines that users who liked the previous three movies also like these three movies.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-126">Mahout determines that users who liked the previous three movies also like these three movies.</span></span>

* <span data-ttu-id="6c2f4-127">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span><span class="sxs-lookup"><span data-stu-id="6c2f4-127">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="6c2f4-128">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-128">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="6c2f4-129">Understanding the data</span><span class="sxs-lookup"><span data-stu-id="6c2f4-129">Understanding the data</span></span>

<span data-ttu-id="6c2f4-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="6c2f4-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="6c2f4-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="6c2f4-133">The `user-ratings.txt` file is used during analysis.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-133">The `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="6c2f4-134">The `moviedb.txt` is used to provide user-friendly text information when viewing the results.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-134">The `moviedb.txt` is used to provide user-friendly text information when viewing the results.</span></span>

<span data-ttu-id="6c2f4-135">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which indicates how highly each user rated a movie.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-135">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which indicates how highly each user rated a movie.</span></span> <span data-ttu-id="6c2f4-136">Here is an example of the data:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-136">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-the-analysis"></a><span data-ttu-id="6c2f4-137">Run the analysis</span><span class="sxs-lookup"><span data-stu-id="6c2f4-137">Run the analysis</span></span>

<span data-ttu-id="6c2f4-138">From an SSH connection to the cluster, use the following command to run the recommendation job:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-138">From an SSH connection to the cluster, use the following command to run the recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="6c2f4-139">The job may take several minutes to complete, and may run multiple MapReduce jobs.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-139">The job may take several minutes to complete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-the-output"></a><span data-ttu-id="6c2f4-140">View the output</span><span class="sxs-lookup"><span data-stu-id="6c2f4-140">View the output</span></span>

1. <span data-ttu-id="6c2f4-141">Once the job completes, use the following command to view the generated output:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-141">Once the job completes, use the following command to view the generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="6c2f4-142">The output appears as follows:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-142">The output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="6c2f4-143">The first column is the `userID`.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-143">The first column is the `userID`.</span></span> <span data-ttu-id="6c2f4-144">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-144">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="6c2f4-145">You can use the output, along with the moviedb.txt, to provide more information on the recommendations.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-145">You can use the output, along with the moviedb.txt, to provide more information on the recommendations.</span></span> <span data-ttu-id="6c2f4-146">First, copy the files locally using the following commands:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-146">First, copy the files locally using the following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="6c2f4-147">This command copies the output data to a file named **recommendations.txt** in the current directory, along with the movie data files.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-147">This command copies the output data to a file named **recommendations.txt** in the current directory, along with the movie data files.</span></span>

3. <span data-ttu-id="6c2f4-148">Use the following command to create a Python script that looks up movie names for the data in the recommendations output:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-148">Use the following command to create a Python script that looks up movie names for the data in the recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="6c2f4-149">When the editor opens, use the following text as the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-149">When the editor opens, use the following text as the contents of the file:</span></span>

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    <span data-ttu-id="6c2f4-150">Press **Ctrl-X**, **Y**, and finally **Enter** to save the data.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-150">Press **Ctrl-X**, **Y**, and finally **Enter** to save the data.</span></span>

4. <span data-ttu-id="6c2f4-151">Run the Python script.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-151">Run the Python script.</span></span> <span data-ttu-id="6c2f4-152">The following command assumes you are in the directory where all the files were downloaded:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-152">The following command assumes you are in the directory where all the files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="6c2f4-153">This command looks at the recommendations generated for user ID 4.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-153">This command looks at the recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="6c2f4-154">The **user-ratings.txt** file is used to retrieve movies that have been rated.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-154">The **user-ratings.txt** file is used to retrieve movies that have been rated.</span></span>

    * <span data-ttu-id="6c2f4-155">The **moviedb.txt** file is used to retrieve the names of the movies.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-155">The **moviedb.txt** file is used to retrieve the names of the movies.</span></span>

    * <span data-ttu-id="6c2f4-156">The **recommendations.txt** is used to retrieve the movie recommendations for this user.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-156">The **recommendations.txt** is used to retrieve the movie recommendations for this user.</span></span>

     <span data-ttu-id="6c2f4-157">The output from this command is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-157">The output from this command is similar to the following text:</span></span>

        <span data-ttu-id="6c2f4-158">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span><span class="sxs-lookup"><span data-stu-id="6c2f4-158">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="6c2f4-159">Delete temporary data</span><span class="sxs-lookup"><span data-stu-id="6c2f4-159">Delete temporary data</span></span>

<span data-ttu-id="6c2f4-160">Mahout jobs do not remove temporary data that is created while processing the job.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-160">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="6c2f4-161">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific path for easy deletion.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-161">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="6c2f4-162">To remove the temp files, use the following command:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-162">To remove the temp files, use the following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="6c2f4-163">If you want to run the command again, you must also delete the output directory.</span><span class="sxs-lookup"><span data-stu-id="6c2f4-163">If you want to run the command again, you must also delete the output directory.</span></span> <span data-ttu-id="6c2f4-164">Use the following to delete this directory:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-164">Use the following to delete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="6c2f4-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c2f4-165">Next steps</span></span>

<span data-ttu-id="6c2f4-166">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6c2f4-166">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="6c2f4-167">Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c2f4-167">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="6c2f4-168">Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c2f4-168">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="6c2f4-169">MapReduce with HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c2f4-169">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]:apache-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
