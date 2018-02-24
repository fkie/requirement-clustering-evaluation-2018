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

clusteralgorithm|distancefunction|usedfields|tfidf|stopwords|interpreted|lemmatized|source| Word2VecAdd|Word2VecAverage|F1WeightedAvg
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

clusteralgorithm|distancefunction|usedfields|tfidf|stopwords|interpreted|lemmatized|source| Word2VecAdd|Word2VecAverage|F1WeightedAvg
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
clusteralgorithm|distancefunction|usedfields|tfidf|stopwords|interpreted|lemmatized|source| Word2VecAdd|Word2VecAverage|F1WeightedAvg
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
clusteralgorithm|distancefunction|usedfields|tfidf|stopwords|interpreted|lemmatized|source| Word2VecAdd|Word2VecAverage|F1WeightedAvg
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
