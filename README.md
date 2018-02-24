# requirement-clustering-evaluation-2018


## Import - external metrics

	sqlite3 external.db << EOF
	
	create table alpha (ClusterAlgorithm, DistanceFunction, UsedFields, Tfidf, StopWords, Lemmatized, Synonyms, GermaNetFunction, Word2VecAdd REAL, Word2VecAverage REAL, F1WeightedAvg REAL, F1WeightedStd REAL, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "alpha.csv" "alpha"
	DELETE from alpha WHERE SeperationAvg = 'SeperationAvg';
	DELETE from alpha WHERE ClusterAlgorithm = '';
	
	create table beta (ClusterAlgorithm, DistanceFunction, UsedFields, Tfidf, StopWords, Lemmatized, Synonyms, GermaNetFunction, Word2VecAdd REAL, Word2VecAverage REAL, F1WeightedAvg REAL, F1WeightedStd REAL, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "beta.csv" "beta"
	DELETE from beta WHERE SeperationAvg = 'SeperationAvg';
	DELETE from beta WHERE ClusterAlgorithm = '';
	
	create table gamma (ClusterAlgorithm, DistanceFunction, UsedFields, Tfidf, StopWords, Lemmatized, Synonyms, GermaNetFunction, Word2VecAdd REAL, Word2VecAverage REAL, F1WeightedAvg REAL, F1WeightedStd REAL, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "gamma.csv" "gamma"
	DELETE from gamma WHERE SeperationAvg = 'SeperationAvg';
	DELETE from gamma WHERE ClusterAlgorithm = '';
	
	create table delta (ClusterAlgorithm, DistanceFunction, UsedFields, Tfidf, StopWords, Lemmatized, Synonyms, GermaNetFunction, Word2VecAdd REAL, Word2VecAverage REAL, F1WeightedAvg REAL, F1WeightedStd REAL, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "delta.csv" "delta"
	DELETE from delta WHERE SeperationAvg = 'SeperationAvg';
	DELETE from delta WHERE ClusterAlgorithm = '';
		
	EOF


## Import - internal metrics

	sqlite3 internal.db << EOF
	
	create table alpha (ClusterAlgorithm, DistanceFunction, Synonyms, GermaNetFunction, Word2VecAdd REAL, Word2VecAverage REAL, k, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "alpha.csv" "alpha"
	DELETE from alpha WHERE SeperationAvg = 'SeperationAvg';
	DELETE from alpha WHERE ClusterAlgorithm = '';
	
	create table beta (ClusterAlgorithm, DistanceFunction, Synonyms, GermaNetFunction, Word2VecAdd REAL, Word2VecAverage REAL, k, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "beta.csv" "beta"
	DELETE from beta WHERE SeperationAvg = 'SeperationAvg';
	DELETE from beta WHERE ClusterAlgorithm = '';
	
	create table gamma (ClusterAlgorithm, DistanceFunction, Synonyms, GermaNetFunction, Word2VecAdd REAL, Word2VecAverage REAL, k, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "gamma.csv" "gamma"
	DELETE from gamma WHERE SeperationAvg = 'SeperationAvg';
	DELETE from gamma WHERE ClusterAlgorithm = '';
	
	create table delta (ClusterAlgorithm, DistanceFunction, Synonyms, GermaNetFunction, Word2VecAdd REAL, Word2VecAverage REAL, k, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "delta.csv" "delta"
	DELETE from delta WHERE SeperationAvg = 'SeperationAvg';
	DELETE from delta WHERE ClusterAlgorithm = '';
			
	EOF


## Verification 

	select "alpha", count(*) from alpha
	UNION ALL 
	select "beta", count(*) from beta
	UNION ALL 
	select "delta", count(*) from delta
	UNION ALL 
	select "gamma", count(*) from gamma


dataset|count
---|---
"alpha"|"2204"
"beta"|"2204"
"delta"|"2204"
"gamma"|"2204"



## Top 10 Performers, external metric
	select clusteralgorithm,distancefunction,usedfields,tfidf,stopwords,lemmatized,synonyms,germanetfunction,Word2VecAdd,Word2VecAverage,F1WeightedAvg from alpha order by F1WeightedAvg desc
	limit 10
	
### alpha

clusteralgorithm|distancefunction|usedfields|tfidf|stopwords|lemmatized|synonyms|germanetfunction|Word2VecAdd|Word2VecAverage|F1WeightedAvg
---|---|---|---|---|---|---|---|---|---|---|
FuzzyCMeans2320|CosineDistance|7|true|true|true|false|false|false|false|0.3443
FuzzyCMeans2320|CosineDistance|7|true|true|true|true|false|false|false|0.3417
KMeans2320|CosineDistance|7|true|true|true|false|false|false|true|0.3209
FuzzyCMeans2320|CosineDistance|7|true|true|true|false|false|true|false|0.3205
KMeans2320|CosineDistance|7|true|true|true|false|false|true|false|0.3165
FuzzyCMeans2320|CosineDistance|7|true|true|true|false|false|false|true|0.3134
FuzzyCMeans2320|CosineDistance|7|true|true|true|true|false|true|false|0.3002
KMeans2320|CosineDistance|7|true|true|true|true|false|false|true|0.299
KMeans2320|EuclideanDistance|7|true|true|true|false|false|false|true|0.299
KMeans2320|CosineDistance|7|true|true|true|false|false|false|false|0.2987


### beta

clusteralgorithm|distancefunction|usedfields|tfidf|stopwords|lemmatized|synonyms|germanetfunction|Word2VecAdd|Word2VecAverage|F1WeightedAvg
---|---|---|---|---|---|---|---|---|---|---|
ClusterART|Not needed|7|true|true|true|true|true|false|false|0.7506
Neural Gas|CosineDistance|7|true|true|true|true|true|true|false|0.5297
Neural Gas|CosineDistance|7|true|true|true|true|true|false|false|0.5285
Neural Gas|CosineDistance|7|true|true|true|true|true|false|true|0.5284
ClusterART|Not needed|7|true|true|true|false|true|false|false|0.5024
Neural Gas|EuclideanDistance|7|true|true|true|true|true|false|true|0.4872
FuzzyCMeans1520|EuclideanDistance|7|true|true|true|false|false|true|false|0.4618
Neural Gas|EuclideanDistance|7|true|true|true|true|false|false|true|0.4617
KMeans1520|WordEmbDistance|7|true|true|true|true|false|false|false|0.459
KMeans1520|WordEmbDistance|7|true|true|true|true|false|false|true|0.459



### gamma
clusteralgorithm|distancefunction|usedfields|tfidf|stopwords|lemmatized|synonyms|germanetfunction|Word2VecAdd|Word2VecAverage|F1WeightedAvg
---|---|---|---|---|---|---|---|---|---|---|
KMeans1720|CosineDistance|7|true|true|true|false|false|false|false|0.5184
KMeans1720|CosineDistance|7|true|true|true|true|false|false|false|0.5044
ClusterART|Not needed|7|true|true|true|true|false|false|false|0.4662
KMeans1720|EuclideanDistance|7|true|true|true|false|false|false|false|0.463
FuzzyCMeans1720|CosineDistance|7|true|true|true|false|false|false|false|0.4353
FuzzyCMeans1720|EuclideanDistance|7|true|true|true|false|false|false|false|0.4352
KMeans1720|EuclideanDistance|7|true|true|true|true|false|false|false|0.4335
FuzzyCMeans1720|CosineDistance|7|true|true|true|true|false|false|false|0.417
FuzzyCMeans1720|EuclideanDistance|7|true|true|true|true|false|false|false|0.4111
KMeans1720|EuclideanDistance|7|true|true|true|false|false|false|true|0.4097


### delta
clusteralgorithm|distancefunction|usedfields|tfidf|stopwords|lemmatized|synonyms|germanetfunction|Word2VecAdd|Word2VecAverage|F1WeightedAvg
---|---|---|---|---|---|---|---|---|---|---|
ClusterART|Not needed|7|true|true|true|true|false|false|false|0.5622
ClusterART|Not needed|7|true|true|true|false|false|false|false|0.5584
Neural Gas|CosineDistance|7|true|true|true|false|false|false|false|0.5102
Neural Gas|CosineDistance|7|true|true|true|true|false|false|false|0.5093
Neural Gas|EuclideanDistance|7|true|true|true|false|false|false|false|0.5082
Neural Gas|EuclideanDistance|7|true|true|true|true|false|false|false|0.5017
KMeans1620|CosineDistance|7|true|true|true|false|false|false|false|0.4604
Neural Gas|EuclideanDistance|7|true|true|true|true|false|false|true|0.4552
Neural Gas|EuclideanDistance|7|true|true|true|false|false|false|true|0.454
KMeans1620|CosineDistance|7|true|true|true|true|false|false|false|0.45

## Top 10 Performers, internal metric

	select k, clusteralgorithm, distancefunction,word2vecadd,word2vecaverage,SilhouetteAvg from alpha order by silhouetteavg desc
	limit 10


### alpha (Human Golden Standard: k=23)
k|clusteralgorithm|distancefunction|word2vecadd|word2vecaverage|SilhouetteAvg
---|---|---|---|---|---|
2|KMeans220|EuclideanDistance|true|false|0.9084
2|KMeans220|EuclideanDistance|true|false|0.9082
2|KMeans220|EuclideanDistance|false|true|0.8006
11|FuzzyCMeans1120|EuclideanDistance|true|false|0.7854
12|FuzzyCMeans1220|EuclideanDistance|true|false|0.7803
13|FuzzyCMeans1320|EuclideanDistance|true|false|0.7681
14|FuzzyCMeans1420|EuclideanDistance|true|false|0.7644
10|FuzzyCMeans1020|EuclideanDistance|true|false|0.7643
15|FuzzyCMeans1520|EuclideanDistance|true|false|0.7584
8|FuzzyCMeans820|EuclideanDistance|true|false|0.7434


### beta (Human Golden Standard: k=15)
k|clusteralgorithm|distancefunction|word2vecadd|word2vecaverage|SilhouetteAvg
---|---|---|---|---|---|
14|KMeans1420|EuclideanDistance|true|false|0.6819
13|KMeans1320|EuclideanDistance|true|false|0.6794
15|KMeans1520|EuclideanDistance|true|false|0.6781
12|KMeans1220|EuclideanDistance|true|false|0.6761
11|KMeans1120|EuclideanDistance|true|false|0.6721
16|KMeans1620|EuclideanDistance|true|false|0.6716
17|KMeans1720|EuclideanDistance|true|false|0.6663
10|KMeans1020|EuclideanDistance|true|false|0.6662
18|KMeans1820|EuclideanDistance|true|false|0.6598
15|FuzzyCMeans1520|EuclideanDistance|true|false|0.6559



### gamma (Human Golden Standard: k=19)
k|clusteralgorithm|distancefunction|word2vecadd|word2vecaverage|SilhouetteAvg
---|---|---|---|---|---|
12|KMeans1220|EuclideanDistance|true|false|0.7102
10|KMeans1020|EuclideanDistance|true|false|0.7081
13|KMeans1320|EuclideanDistance|true|false|0.7073
11|KMeans1120|EuclideanDistance|true|false|0.7053
14|KMeans1420|EuclideanDistance|true|false|0.7039
9|KMeans920|EuclideanDistance|true|false|0.7036
15|KMeans1520|EuclideanDistance|true|false|0.6983
8|KMeans820|EuclideanDistance|true|false|0.6957
16|KMeans1620|EuclideanDistance|true|false|0.6919
11|KMeans1120|EuclideanDistance|true|false|0.6881


### delta (Human Golden Standard: k=16)
k|clusteralgorithm|distancefunction|word2vecadd|word2vecaverage|SilhouetteAvg
---|---|---|---|---|---|
16|FuzzyCMeans1620|EuclideanDistance|true|false|0.7195
15|FuzzyCMeans1520|EuclideanDistance|true|false|0.7181
13|FuzzyCMeans1320|EuclideanDistance|true|false|0.7169
17|FuzzyCMeans1720|EuclideanDistance|true|false|0.7149
14|FuzzyCMeans1420|EuclideanDistance|true|false|0.7142
14|KMeans1420|EuclideanDistance|true|false|0.714
12|FuzzyCMeans1220|EuclideanDistance|true|false|0.7137
13|KMeans1320|EuclideanDistance|true|false|0.7117
12|KMeans1220|EuclideanDistance|true|false|0.7104
16|KMeans1620|EuclideanDistance|true|false|0.7103



## Correlation between Silhouette and F1

	select SilhouetteAvg,F1WeightedAvg from alpha
	where distancefunction <> "WordEmbDistance" -- Not supported distance function


### alpha

	CORREL(SilhouetteAvg, F1WeightedAvg) = -0.002879579897854

### beta

	CORREL(SilhouetteAvg, F1WeightedAvg) = -0.321574158661689

### gamma

	CORREL(SilhouetteAvg, F1WeightedAvg) = -0.211575766205108

### delta
	CORREL(SilhouetteAvg, F1WeightedAvg) = -0.195570970269602


## Best performances per parameter (external)

	select ClusterAlgorithm, DistanceFunction, Synonyms, Tfidf, Synonyms, GermaNetFunction, Word2VecAdd, Word2VecAverage, SilhouetteAvg, max(F1WeightedAvg) BestF1 from alpha
	group by ClusterAlgorithm
	order by BestF1 desc


### alpha
ClusterAlgorithm|DistanceFunction|Synonyms|Tfidf|Synonyms|GermaNetFunction|Word2VecAdd|Word2VecAverage|SilhouetteAvg|BestF1
---|---|---|---|---|---|---|---|---|---|
FuzzyCMeans2320|CosineDistance|false|true|false|false|false|false|0.0847|0.3443
KMeans2320|CosineDistance|false|true|false|false|false|true|0.0374|0.3209
Neural Gas|EuclideanDistance|false|true|false|true|false|true|0.0893|0.2475
ClusterART|Not needed|false|true|false|false|false|false|0.1943|0.2383


### beta
ClusterAlgorithm|DistanceFunction|Synonyms|Tfidf|Synonyms|GermaNetFunction|Word2VecAdd|Word2VecAverage|SilhouetteAvg|BestF1
---|---|---|---|---|---|---|---|---|---|
ClusterART|Not needed|true|true|true|true|false|false|0.0189|0.7506
Neural Gas|CosineDistance|true|true|true|true|true|false|-0.0464|0.5297
FuzzyCMeans1520|EuclideanDistance|false|true|false|false|true|false|0.022|0.4618
KMeans1520|WordEmbDistance|true|true|true|false|false|false|-1.0|0.459


### gamma
ClusterAlgorithm|DistanceFunction|Synonyms|Tfidf|Synonyms|GermaNetFunction|Word2VecAdd|Word2VecAverage|SilhouetteAvg|BestF1
---|---|---|---|---|---|---|---|---|---|
KMeans1720|CosineDistance|false|true|false|false|false|false|0.1451|0.5184
ClusterART|Not needed|true|true|true|false|false|false|0.2436|0.4662
FuzzyCMeans1720|CosineDistance|false|true|false|false|false|false|0.1041|0.4353
Neural Gas|CosineDistance|true|true|true|false|false|true|0.0701|0.4083

### delta
ClusterAlgorithm|DistanceFunction|Synonyms|Tfidf|Synonyms|GermaNetFunction|Word2VecAdd|Word2VecAverage|SilhouetteAvg|BestF1
---|---|---|---|---|---|---|---|---|---|
ClusterART|Not needed|true|true|true|false|false|false|0.2014|0.5622
Neural Gas|CosineDistance|false|true|false|false|false|false|0.0636|0.5102
KMeans1620|CosineDistance|false|true|false|false|false|false|0.1435|0.4604
FuzzyCMeans1620|EuclideanDistance|false|true|false|false|false|true|0.0227|0.4394


## Best performances per parameter (internal)

	select ClusterAlgorithm, k, DistanceFunction, Synonyms, Synonyms, GermaNetFunction, Word2VecAdd, Word2VecAverage, max(SilhouetteAvg) from alpha
	group by ClusterAlgorithm
	order by SilhouetteAvg desc
	
	
### alpha

ClusterAlgorithm|k|DistanceFunction|Synonyms|Synonyms|GermaNetFunction|Word2VecAdd|Word2VecAverage|Best SilhouetteAvg|
---|---|---|---|---|---|---|---|---| 
KMeans220|2|EuclideanDistance|true|true|false|true|false|0.9084
FuzzyCMeans1120|11|EuclideanDistance|true|true|true|true|false|0.7854
FuzzyCMeans1220|12|EuclideanDistance|true|true|true|true|false|0.7803
FuzzyCMeans1320|13|EuclideanDistance|true|true|true|true|false|0.7681
FuzzyCMeans1420|14|EuclideanDistance|true|true|true|true|false|0.7644
FuzzyCMeans1020|10|EuclideanDistance|true|true|true|true|false|0.7643
FuzzyCMeans1520|15|EuclideanDistance|true|true|true|true|false|0.7584
FuzzyCMeans820|8|EuclideanDistance|true|true|true|true|false|0.7434
FuzzyCMeans1620|16|EuclideanDistance|true|true|true|true|false|0.7376
FuzzyCMeans920|9|EuclideanDistance|true|true|true|true|false|0.7375
KMeans1020|10|EuclideanDistance|true|true|true|true|false|0.7351
KMeans920|9|EuclideanDistance|true|true|true|true|false|0.7344
KMeans1120|11|EuclideanDistance|true|true|true|true|false|0.7332
FuzzyCMeans1720|17|EuclideanDistance|true|true|true|true|false|0.7295
KMeans1220|12|EuclideanDistance|true|true|true|true|false|0.7289
KMeans1320|13|EuclideanDistance|false|false|true|true|false|0.7282
KMeans820|8|EuclideanDistance|true|true|true|true|false|0.726
KMeans1420|14|EuclideanDistance|false|false|true|true|false|0.7251
KMeans1520|15|EuclideanDistance|false|false|true|true|false|0.7196
KMeans1620|16|EuclideanDistance|false|false|true|true|false|0.7166
KMeans1720|17|EuclideanDistance|false|false|true|true|false|0.715
KMeans720|7|EuclideanDistance|true|true|true|true|false|0.713
FuzzyCMeans720|7|EuclideanDistance|true|true|true|true|false|0.7085
KMeans1820|18|EuclideanDistance|false|false|true|true|false|0.7074
FuzzyCMeans1820|18|EuclideanDistance|true|true|true|true|false|0.7062
FuzzyCMeans1920|19|EuclideanDistance|true|true|true|true|false|0.7059
KMeans1920|19|EuclideanDistance|false|false|true|true|false|0.7047
KMeans2020|20|EuclideanDistance|false|false|true|true|false|0.7005
KMeans2120|21|EuclideanDistance|false|false|true|true|false|0.6994
FuzzyCMeans2020|20|EuclideanDistance|true|true|true|true|false|0.6975
KMeans2220|22|EuclideanDistance|false|false|true|true|false|0.6967
KMeans2320|23|EuclideanDistance|false|false|true|true|false|0.689
KMeans620|6|EuclideanDistance|true|true|true|true|false|0.6854
KMeans2420|24|EuclideanDistance|false|false|true|true|false|0.683
KMeans2520|25|EuclideanDistance|false|false|true|true|false|0.6801
FuzzyCMeans2120|21|EuclideanDistance|true|true|true|true|false|0.6797
FuzzyCMeans2220|22|EuclideanDistance|true|true|true|true|false|0.6777
FuzzyCMeans620|6|EuclideanDistance|true|true|true|true|false|0.6721
KMeans2620|26|EuclideanDistance|false|false|true|true|false|0.6719
FuzzyCMeans2320|23|EuclideanDistance|true|true|true|true|false|0.6656
KMeans2720|27|EuclideanDistance|false|false|true|true|false|0.6606
KMeans2820|28|EuclideanDistance|false|false|true|true|false|0.6566
FuzzyCMeans2420|24|EuclideanDistance|true|true|true|true|false|0.6549
KMeans2920|29|EuclideanDistance|false|false|true|true|false|0.6487
KMeans3020|30|EuclideanDistance|false|false|true|true|false|0.6461
FuzzyCMeans2520|25|EuclideanDistance|true|true|true|true|false|0.6443
FuzzyCMeans2620|26|EuclideanDistance|true|true|true|true|false|0.6428
KMeans520|5|EuclideanDistance|true|true|true|true|false|0.6395
FuzzyCMeans2720|27|EuclideanDistance|true|true|true|true|false|0.6279
FuzzyCMeans2820|28|EuclideanDistance|true|true|true|true|false|0.6222
FuzzyCMeans520|5|EuclideanDistance|true|true|true|true|false|0.6151
FuzzyCMeans2920|29|EuclideanDistance|true|true|true|true|false|0.6109
KMeans420|4|EuclideanDistance|true|true|true|false|true|0.6086
FuzzyCMeans3020|30|EuclideanDistance|true|true|true|true|false|0.5966
FuzzyCMeans220|2|EuclideanDistance|false|false|true|false|true|0.5666
KMeans320|3|EuclideanDistance|true|true|true|true|false|0.5651
FuzzyCMeans420|4|EuclideanDistance|false|false|true|false|true|0.5507
Neural Gas|2|EuclideanDistance|true|true|true|false|true|0.545
FuzzyCMeans320|3|EuclideanDistance|true|true|true|false|true|0.5406
ClusterART|27|Not needed|false|false|false|false|false|0.2134


### beta

ClusterAlgorithm|k|DistanceFunction|Synonyms|Synonyms|GermaNetFunction|Word2VecAdd|Word2VecAverage|Best SilhouetteAvg|
---|---|---|---|---|---|---|---|---| 
KMeans1420|14|EuclideanDistance|false|false|true|true|false|0.6819
KMeans1320|13|EuclideanDistance|false|false|true|true|false|0.6794
KMeans1520|15|EuclideanDistance|false|false|true|true|false|0.6781
KMeans1220|12|EuclideanDistance|false|false|true|true|false|0.6761
KMeans1120|11|EuclideanDistance|false|false|true|true|false|0.6721
KMeans1620|16|EuclideanDistance|false|false|true|true|false|0.6716
KMeans1720|17|EuclideanDistance|false|false|true|true|false|0.6663
KMeans1020|10|EuclideanDistance|false|false|true|true|false|0.6662
KMeans1820|18|EuclideanDistance|false|false|true|true|false|0.6598
FuzzyCMeans1520|15|EuclideanDistance|true|true|true|true|false|0.6559
KMeans1920|19|EuclideanDistance|false|false|true|true|false|0.652
FuzzyCMeans1420|14|EuclideanDistance|true|true|true|true|false|0.6509
KMeans920|9|EuclideanDistance|false|false|true|true|false|0.6509
FuzzyCMeans1620|16|EuclideanDistance|true|true|true|true|false|0.6482
KMeans2020|20|EuclideanDistance|false|false|true|true|false|0.6458
FuzzyCMeans1320|13|EuclideanDistance|true|true|true|true|false|0.6435
FuzzyCMeans1720|17|EuclideanDistance|true|true|true|true|false|0.6392
FuzzyCMeans1220|12|EuclideanDistance|true|true|true|true|false|0.6362
KMeans2120|21|EuclideanDistance|false|false|true|true|false|0.6357
KMeans820|8|EuclideanDistance|true|true|true|true|false|0.6311
FuzzyCMeans1820|18|EuclideanDistance|true|true|true|true|false|0.6297
KMeans2220|22|EuclideanDistance|false|false|true|true|false|0.6278
KMeans2320|23|EuclideanDistance|false|false|true|true|false|0.6191
FuzzyCMeans1920|19|EuclideanDistance|true|true|true|true|false|0.615
FuzzyCMeans920|9|EuclideanDistance|true|true|true|true|false|0.6149
FuzzyCMeans720|7|EuclideanDistance|true|true|true|true|false|0.6127
KMeans720|7|EuclideanDistance|true|true|true|true|false|0.6117
FuzzyCMeans2020|20|EuclideanDistance|true|true|true|true|false|0.6075
KMeans2420|24|EuclideanDistance|false|false|true|true|false|0.6071
FuzzyCMeans1020|10|EuclideanDistance|true|true|true|true|false|0.6063
FuzzyCMeans1120|11|EuclideanDistance|false|false|true|true|false|0.6057
FuzzyCMeans620|6|EuclideanDistance|true|true|true|true|false|0.6057
KMeans2520|25|EuclideanDistance|false|false|true|true|false|0.6009
FuzzyCMeans820|8|EuclideanDistance|true|true|true|true|false|0.6004
FuzzyCMeans2120|21|EuclideanDistance|true|true|true|true|false|0.5949
KMeans2620|26|EuclideanDistance|false|false|true|true|false|0.5908
KMeans620|6|EuclideanDistance|true|true|true|true|false|0.5868
KMeans2720|27|EuclideanDistance|false|false|true|true|false|0.5849
FuzzyCMeans2220|22|EuclideanDistance|true|true|true|true|false|0.5811
FuzzyCMeans220|2|EuclideanDistance|false|false|true|false|true|0.579
KMeans2820|28|EuclideanDistance|false|false|true|true|false|0.5785
FuzzyCMeans2320|23|EuclideanDistance|true|true|true|true|false|0.5763
KMeans2920|29|EuclideanDistance|false|false|true|true|false|0.571
KMeans220|2|EuclideanDistance|false|false|true|false|true|0.5709
KMeans520|5|EuclideanDistance|false|false|true|false|true|0.5702
KMeans3020|30|EuclideanDistance|false|false|true|true|false|0.5654
FuzzyCMeans2420|24|EuclideanDistance|true|true|true|true|false|0.5599
Neural Gas|2|EuclideanDistance|false|false|true|false|true|0.5588
FuzzyCMeans2520|25|EuclideanDistance|true|true|true|true|false|0.5537
KMeans320|3|EuclideanDistance|false|false|true|false|true|0.5533
FuzzyCMeans2620|26|EuclideanDistance|true|true|true|true|false|0.5492
KMeans420|4|EuclideanDistance|true|true|true|true|false|0.5477
FuzzyCMeans320|3|EuclideanDistance|false|false|true|false|true|0.5346
FuzzyCMeans520|5|EuclideanDistance|false|false|true|false|true|0.5323
FuzzyCMeans2720|27|EuclideanDistance|true|true|true|true|false|0.5319
FuzzyCMeans420|4|EuclideanDistance|false|false|true|false|true|0.5243
FuzzyCMeans2820|28|EuclideanDistance|true|true|true|true|false|0.5177
FuzzyCMeans2920|29|EuclideanDistance|true|true|true|true|false|0.5044
FuzzyCMeans3020|30|EuclideanDistance|true|true|true|true|false|0.5016
ClusterART|2|Not needed|false|false|false|false|false|0.2176



### gamma

ClusterAlgorithm|k|DistanceFunction|Synonyms|Synonyms|GermaNetFunction|Word2VecAdd|Word2VecAverage|Best SilhouetteAvg|
---|---|---|---|---|---|---|---|---| 
KMeans1220|12|EuclideanDistance|true|true|true|true|false|0.7102
KMeans1020|10|EuclideanDistance|true|true|true|true|false|0.7081
KMeans1320|13|EuclideanDistance|true|true|true|true|false|0.7073
KMeans1120|11|EuclideanDistance|true|true|true|true|false|0.7053
KMeans1420|14|EuclideanDistance|true|true|true|true|false|0.7039
KMeans920|9|EuclideanDistance|true|true|true|true|false|0.7036
KMeans1520|15|EuclideanDistance|true|true|true|true|false|0.6983
KMeans820|8|EuclideanDistance|true|true|true|true|false|0.6957
KMeans1620|16|EuclideanDistance|true|true|true|true|false|0.6919
KMeans1720|17|EuclideanDistance|true|true|true|true|false|0.6843
KMeans1820|18|EuclideanDistance|true|true|true|true|false|0.6827
FuzzyCMeans1720|17|EuclideanDistance|true|true|true|true|false|0.6799
FuzzyCMeans1620|16|EuclideanDistance|true|true|true|true|false|0.6795
KMeans720|7|EuclideanDistance|true|true|true|true|false|0.6784
KMeans1920|19|EuclideanDistance|true|true|true|true|false|0.6755
FuzzyCMeans620|6|EuclideanDistance|true|true|true|true|false|0.6714
FuzzyCMeans1520|15|EuclideanDistance|true|true|true|true|false|0.6707
FuzzyCMeans1920|19|EuclideanDistance|true|true|true|true|false|0.667
KMeans2020|20|EuclideanDistance|true|true|true|true|false|0.6655
FuzzyCMeans1820|18|EuclideanDistance|true|true|true|true|false|0.6639
FuzzyCMeans1320|13|EuclideanDistance|true|true|true|true|false|0.66
KMeans2120|21|EuclideanDistance|true|true|true|true|false|0.6597
FuzzyCMeans1420|14|EuclideanDistance|true|true|true|true|false|0.6593
KMeans620|6|EuclideanDistance|true|true|true|true|false|0.6584
KMeans2220|22|EuclideanDistance|true|true|true|true|false|0.6569
FuzzyCMeans2020|20|EuclideanDistance|true|true|true|true|false|0.6515
KMeans2320|23|EuclideanDistance|true|true|true|true|false|0.6512
KMeans2420|24|EuclideanDistance|true|true|true|true|false|0.6496
FuzzyCMeans1220|12|EuclideanDistance|true|true|true|true|false|0.6468
FuzzyCMeans820|8|EuclideanDistance|false|false|true|true|false|0.6453
KMeans2520|25|EuclideanDistance|true|true|true|true|false|0.6411
FuzzyCMeans1020|10|EuclideanDistance|true|true|true|true|false|0.6394
FuzzyCMeans2120|21|EuclideanDistance|false|false|true|true|false|0.6392
KMeans2620|26|EuclideanDistance|true|true|true|true|false|0.6385
KMeans520|5|EuclideanDistance|true|true|true|true|false|0.6366
KMeans2720|27|EuclideanDistance|true|true|true|true|false|0.6338
FuzzyCMeans2220|22|EuclideanDistance|false|false|true|true|false|0.6312
FuzzyCMeans2320|23|EuclideanDistance|false|false|true|true|false|0.6312
KMeans2820|28|EuclideanDistance|true|true|true|true|false|0.6285
FuzzyCMeans1120|11|EuclideanDistance|true|true|true|true|false|0.6259
FuzzyCMeans520|5|EuclideanDistance|true|true|true|false|true|0.6258
FuzzyCMeans2420|24|EuclideanDistance|false|false|true|true|false|0.6253
KMeans2920|29|EuclideanDistance|true|true|true|true|false|0.6246
FuzzyCMeans920|9|EuclideanDistance|true|true|true|true|false|0.6243
FuzzyCMeans2520|25|EuclideanDistance|false|false|true|true|false|0.6213
FuzzyCMeans720|7|EuclideanDistance|true|true|true|true|false|0.6202
KMeans3020|30|EuclideanDistance|true|true|true|true|false|0.6189
FuzzyCMeans2620|26|EuclideanDistance|false|false|true|true|false|0.6027
KMeans420|4|EuclideanDistance|false|false|true|false|true|0.6004
KMeans220|2|EuclideanDistance|false|false|true|true|false|0.5975
KMeans320|3|EuclideanDistance|true|true|true|false|true|0.596
FuzzyCMeans220|2|EuclideanDistance|false|false|true|true|false|0.5943
FuzzyCMeans2720|27|EuclideanDistance|false|false|true|true|false|0.594
FuzzyCMeans2820|28|EuclideanDistance|false|false|true|true|false|0.5865
FuzzyCMeans420|4|EuclideanDistance|true|true|true|false|true|0.5813
Neural Gas|2|EuclideanDistance|true|true|true|true|false|0.5772
FuzzyCMeans2920|29|EuclideanDistance|false|false|true|true|false|0.5711
FuzzyCMeans320|3|EuclideanDistance|true|true|true|true|false|0.5697
FuzzyCMeans3020|30|EuclideanDistance|false|false|true|true|false|0.5594
ClusterART|13|Not needed|false|false|false|false|false|0.3186



### delta

ClusterAlgorithm|k|DistanceFunction|Synonyms|Synonyms|GermaNetFunction|Word2VecAdd|Word2VecAverage|Best SilhouetteAvg|
---|---|---|---|---|---|---|---|---| 
FuzzyCMeans1620|16|EuclideanDistance|true|true|true|true|false|0.7195
FuzzyCMeans1520|15|EuclideanDistance|true|true|true|true|false|0.7181
FuzzyCMeans1320|13|EuclideanDistance|true|true|true|true|false|0.7169
FuzzyCMeans1720|17|EuclideanDistance|true|true|true|true|false|0.7149
FuzzyCMeans1420|14|EuclideanDistance|true|true|true|true|false|0.7142
KMeans1420|14|EuclideanDistance|true|true|true|true|false|0.714
FuzzyCMeans1220|12|EuclideanDistance|true|true|true|true|false|0.7137
KMeans1320|13|EuclideanDistance|true|true|true|true|false|0.7117
KMeans1220|12|EuclideanDistance|true|true|true|true|false|0.7104
KMeans1620|16|EuclideanDistance|true|true|true|true|false|0.7103
KMeans1120|11|EuclideanDistance|true|true|true|true|false|0.7099
KMeans1520|15|EuclideanDistance|true|true|true|true|false|0.7094
FuzzyCMeans1820|18|EuclideanDistance|true|true|true|true|false|0.7093
FuzzyCMeans1920|19|EuclideanDistance|true|true|true|true|false|0.7067
KMeans1720|17|EuclideanDistance|true|true|true|true|false|0.7041
KMeans1020|10|EuclideanDistance|true|true|true|true|false|0.7031
KMeans1820|18|EuclideanDistance|true|true|true|true|false|0.7012
KMeans1920|19|EuclideanDistance|true|true|true|true|false|0.6988
KMeans2020|20|EuclideanDistance|true|true|true|true|false|0.6964
FuzzyCMeans2020|20|EuclideanDistance|true|true|true|true|false|0.6914
KMeans920|9|EuclideanDistance|true|true|true|true|false|0.6913
KMeans2120|21|EuclideanDistance|true|true|true|true|false|0.6906
FuzzyCMeans2120|21|EuclideanDistance|true|true|true|true|false|0.6866
KMeans2220|22|EuclideanDistance|true|true|true|true|false|0.6851
KMeans2320|23|EuclideanDistance|true|true|true|true|false|0.6789
KMeans820|8|EuclideanDistance|true|true|true|true|false|0.6786
FuzzyCMeans1120|11|EuclideanDistance|false|false|true|true|false|0.6782
KMeans2420|24|EuclideanDistance|true|true|true|true|false|0.6777
FuzzyCMeans2220|22|EuclideanDistance|true|true|true|true|false|0.6748
FuzzyCMeans1020|10|EuclideanDistance|false|false|true|true|false|0.6744
KMeans2520|25|EuclideanDistance|true|true|true|true|false|0.6713
KMeans2620|26|EuclideanDistance|true|true|true|true|false|0.6657
FuzzyCMeans2320|23|EuclideanDistance|true|true|true|true|false|0.6652
KMeans2720|27|EuclideanDistance|true|true|true|true|false|0.6641
KMeans2820|28|EuclideanDistance|true|true|true|true|false|0.6586
FuzzyCMeans920|9|EuclideanDistance|false|false|true|true|false|0.6577
KMeans720|7|EuclideanDistance|false|false|true|true|false|0.6571
KMeans2920|29|EuclideanDistance|true|true|true|true|false|0.6548
FuzzyCMeans620|6|EuclideanDistance|false|false|true|false|true|0.6518
FuzzyCMeans2420|24|EuclideanDistance|false|false|true|true|false|0.6507
KMeans3020|30|EuclideanDistance|true|true|true|true|false|0.6494
FuzzyCMeans820|8|EuclideanDistance|true|true|true|true|false|0.6493
FuzzyCMeans2520|25|EuclideanDistance|false|false|true|true|false|0.6477
FuzzyCMeans2620|26|EuclideanDistance|false|false|true|true|false|0.6462
FuzzyCMeans2720|27|EuclideanDistance|false|false|true|true|false|0.6413
FuzzyCMeans720|7|EuclideanDistance|false|false|true|true|false|0.6395
KMeans620|6|EuclideanDistance|true|true|true|true|false|0.6378
FuzzyCMeans2820|28|EuclideanDistance|false|false|true|true|false|0.6359
FuzzyCMeans2920|29|EuclideanDistance|false|false|true|true|false|0.6153
KMeans520|5|EuclideanDistance|false|false|true|false|true|0.6056
FuzzyCMeans3020|30|EuclideanDistance|false|false|true|true|false|0.6017
KMeans220|2|EuclideanDistance|true|true|true|true|false|0.5973
FuzzyCMeans220|2|EuclideanDistance|true|true|true|false|true|0.5849
Neural Gas|2|EuclideanDistance|false|false|true|false|true|0.5828
KMeans420|4|EuclideanDistance|true|true|true|true|false|0.569
KMeans320|3|EuclideanDistance|false|false|true|false|true|0.5522
FuzzyCMeans420|4|EuclideanDistance|false|false|true|false|true|0.5503
FuzzyCMeans320|3|EuclideanDistance|false|false|true|false|true|0.5451
FuzzyCMeans520|5|EuclideanDistance|false|false|true|false|true|0.5213
ClusterART|10|Not needed|false|false|true|false|false|0.4338



## k vs. Silhouette, Top 15

		select k, max(SilhouetteAvg) from delta group by k order by SilhouetteAvg desc
	limit 15



### alpha

![](kvssilhouette-alpha.png)

### beta

![](kvssilhouette-beta.png)

### gamma

![](kvssilhouette-gamma.png)


### delta

![](kvssilhouette-delta.png)