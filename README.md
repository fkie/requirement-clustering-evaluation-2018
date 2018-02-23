# requirement-clustering-evaluation-2018


## Import - external metrics

	sqlite3 external.db << EOF
	
	create table alpha (ClusterAlgorithm, DistanceFunction, UsedFields, Tfidf, StopWords, Interpreted, Lemmatized, Source, Synonyms, GermaNetFunction, F1WeightedAvg REAL, F1WeightedStd REAL, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "alpha.csv" "alpha"
	DELETE from alpha WHERE SeperationAvg = 'SeperationAvg';
	DELETE from alpha WHERE ClusterAlgorithm = '';
	
	create table beta (ClusterAlgorithm, DistanceFunction, UsedFields, Tfidf, StopWords, Interpreted, Lemmatized, Source, Synonyms, GermaNetFunction, F1WeightedAvg REAL, F1WeightedStd REAL, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "beta.csv" "beta"
	DELETE from beta WHERE SeperationAvg = 'SeperationAvg';
	DELETE from beta WHERE ClusterAlgorithm = '';
	
	create table gamma (ClusterAlgorithm, DistanceFunction, UsedFields, Tfidf, StopWords, Interpreted, Lemmatized, Source, Synonyms, GermaNetFunction, F1WeightedAvg REAL, F1WeightedStd REAL, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "gamma.csv" "gamma"
	DELETE from gamma WHERE SeperationAvg = 'SeperationAvg';
	DELETE from gamma WHERE ClusterAlgorithm = '';
	
	create table delta (ClusterAlgorithm, DistanceFunction, UsedFields, Tfidf, StopWords, Interpreted, Lemmatized, Source, Synonyms, GermaNetFunction, F1WeightedAvg REAL, F1WeightedStd REAL, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "delta.csv" "delta"
	DELETE from delta WHERE SeperationAvg = 'SeperationAvg';
	DELETE from delta WHERE ClusterAlgorithm = '';
		
	create table zeta (ClusterAlgorithm, DistanceFunction, UsedFields, Tfidf, StopWords, Interpreted, Lemmatized, Source, Synonyms, GermaNetFunction, F1WeightedAvg REAL, F1WeightedStd REAL, CohesionAvg REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "zeta.csv" "zeta"
	DELETE from zeta WHERE SeperationAvg = 'SeperationAvg';
	DELETE from zeta WHERE ClusterAlgorithm = '';
	
	EOF


## Import - internal metrics

	sqlite3 internal.db << EOF
	
	create table alpha (ClusterAlgorithm, DistanceFunction, Synonyms, GermaNetFunction, Word2VecAdd, Word2VecAverage, k, CohesionAvg	REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "alpha.csv" "alpha"
	DELETE from alpha WHERE SeperationAvg = 'SeperationAvg';
	DELETE from alpha WHERE ClusterAlgorithm = '';
	
	create table beta (ClusterAlgorithm, DistanceFunction, Synonyms, GermaNetFunction, Word2VecAdd, Word2VecAverage, k, CohesionAvg	REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "beta.csv" "beta"
	DELETE from beta WHERE SeperationAvg = 'SeperationAvg';
	DELETE from beta WHERE ClusterAlgorithm = '';
	
	create table gamma (ClusterAlgorithm, DistanceFunction, Synonyms, GermaNetFunction, Word2VecAdd, Word2VecAverage, k, CohesionAvg	REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
	.separator ";"
	.import "gamma.csv" "gamma"
	DELETE from gamma WHERE SeperationAvg = 'SeperationAvg';
	DELETE from gamma WHERE ClusterAlgorithm = '';
	
	create table delta (ClusterAlgorithm, DistanceFunction, Synonyms, GermaNetFunction, Word2VecAdd, Word2VecAverage, k, CohesionAvg	REAL, CohesionStd REAL, SeperationAvg REAL, SeperationStd REAL, SilhouetteAvg REAL, SilhouetteStd REAL, RuntimeAvg REAL);
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



## Top 10 Performers (internal metric)

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
