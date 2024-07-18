---
title: About the Alpha and Beta Diversity Analysis Tutorial
---

This Alpha and Beta Diversity Community Tutorial (run using QIIME 2017.12) walks you through analyzing the alpha and beta diversity of a sample dataset. Below you will find a link to a small test dataset to download and use in this tutorial.

## Files used in tutorial

The following files, derived from the [_Moving Pictures tutorial_](https://docs.qiime2.org/2017.12/tutorials/moving-pictures/), are used in this document.

- [table.qza](https://docs.qiime2.org/2017.12/data/tutorials/moving-pictures/table.qza)
- [rooted-tree.qza](https://docs.qiime2.org/2017.12/data/tutorials/moving-pictures/rooted-tree.qza)

## Alpha Diversity Analysis

The `alpha` and `alpha-phylogenetic` methods compute a user-specified alpha diversity metric for all samples in a feature table.

Phylogenetic alpha diversity metrics (in this case, Faith’s Phylogenetic Diversity), can be run with the following command:

```bash
qiime diversity alpha-phylogenetic \
  --i-table table.qza \
  --i-phylogeny rooted-tree.qza \
  --p-metric faith_pd \
  --o-alpha-diversity faith_pd_vector.qza
```

Non-phylogenetic alpha diversity metrics (in this case, Observed OTUs), can be run with the following command:

```bash
qiime diversity alpha \
  --i-table table.qza \
  --p-metric observed_otus \
  --o-alpha-diversity observed_otus_vector.qza
```

The `--i-table` input provides the feature table containing the samples for which the alpha diversity metric will be computed. The `--i-phylogeny` input provides the phylogenetic tree containing the tip identifiers that correspond to the feature identifiers in the table, and is only used for the `alpha-phylogenetic` command (i.e., when computing phylogenetic diversity metrics. The `--p-metric` parameter specifies the alpha diversity metric to be run. The `--o-alpha-diversity` output specifies the output file.

To compute a different alpha diversity metric, change the `--p-metric` parameter to the one that corresponds to the metric you want to compute. The following list provides information on the available alpha diversity metrics in QIIME 2.

- **Abundance-based Coverage Estimator (ACE) metric**: Calculates the ACE metric
  - Estimates species richness using a correction factor
  - **`--p-metric`: ace**
  - _Chao, A. and Lee, S.M.. (1992). “Estimating the number of classes via sample coverage”. Journal of the American Statistical Association. (87): 210-217._
- **Berger-Parker Dominance Index**: Calculates Berger-Parker dominance index
  - Relative richness of the abundant species
  - **`--p-metric`: berger_parker_d**
  - _Berger, W.H. and Parker, F.L. (1970). “Diversity of planktonic Foraminifera in deep sea sediments”. Science. (168): 1345-1347._
- **Brillouin’s index**: Calculates Brillouin’s index
  - Measures the diversity of the species present
  - Use when randomness can’t be guaranteed
  - **`--p-metric`: brillouin_d**
  - _Pielou, E. C. (1975). Ecological Diversity. New York, Wiley InterScience._
- **Chao1 confidence interval**: Calculates chao1 confidence interval
  - Confidence interval for richness estimator, Chao1
  - **`--p-metric`: chao1_ci**
  - _Colwell, R.K., Mao, C.X., Chang, J. (2004). “Interpolating, extrapolating, and comparing incidence-based species accumulation curves.” Ecology. (85), 2717-2727._
- **Chao1 index**: Calculates Chao1 index
  - Estimates diversity from abundant data
  - Estimates number of rare taxa missed from undersampling
  - **`--p-metric`: chao1**
  - \*Chao, A. (1984). “Non-parametric estimation of the number of classes in a population”.
- **Dominance measure**: Calculates dominance measure\*\*
  - How equally the taxa are presented
  - **`--p-metric`: dominance**
- **Effective Number of Species (ENS)/Probability of intra-or interspecific encounter (PIE) metric**: Calculates Effective Number of Species (ENS)/Probability of intra-or interspecific encounter (PIE) metric
  - Shows how absolute amount of species, relative abundances of species, and their intraspecific clustering affect differences in biodiversity among communities
  - **`--p-metric`: enspie**
  - _Chase, J.M., and Knight, R. (2013). “Scale-dependent effect sizes of ecological drivers on biodiversity: why standardised sampling is not enough”. Ecology Letters (16): 17-26._
- **Etsy confidence interval**: Calculates Esty’s confidence interval
  - Confidence interval for how many singletons in total individuals
  - **`--p-metric`: etsy_ci**
  - _Esty, W. W. (1983). “A normal limit law for a nonparametric estimator of the coverage of a random sample”. Ann Statist. (11): 905-912._
- **Faith’s phylogenetic diversity**: Calculates faith’s phylogenetic diversity
  - Measures of biodiversity that incorporates phylogenetic difference between species
  - Sum of length of branches
  - **`--p-metric`: faith_pd**
  - _Faith. D.P. (1992). “Conservation evaluation and phylogenetic diversity”. Biological Conservation. (61) 1-10._
- **Fisher’s index**: Calculates Fisher’s index
  - Relationship between the number of species and the abundance of each species
  - **`--p-metric`: fisher_alpha**
  - _Fisher, R.A., Corbet, A.S. and Williams, C.B. (1943). “The relation between the number of species and the number of individuals in a random sample of an animal population”. Journal of Animal Ecology. (12): 42-58._
- **Gini index**: Calculates Gini index
  - Measures species abundance
  - Assumes that the sampling is accurate and that additional data would fall on linear gradients between the values of the given data
  - **`--p-metric`: gini_index**
  - _Gini, C. (1912). “Variability and Mutability”. C. Cuppini, Bologna. 156._
- **Good’s coverage of counts**: Calculates Good’s coverage of counts.
  - Estimates the percent of an entire species that is represented in a sample
  - **`--p-metric`: goods_coverage**
  - _Good. I.J (1953) “The populations frequency of Species and the Estimation of Populations Parameters”. Biometrika. 40(3/4):237-264_
- **Heip’s evenness measure**: Calculates Heip’s evenness measure.
  - Removes dependency on species number
  - **`--p-metric`: heip_e**
  - _Heip, C. (1974). “A new index measuring evenness”. J. Mar. Biol. Ass. UK. (54): 555-557._
- **Kempton-Taylor Q index**: Calculates Kempton-Taylor Q index
  - Measured diversity based off the distributions of species
  - Makes abundance curve based off all species and IQR is used to measure diversity
  - **`--p-metric`: kempton_taylor_q**
  - _Kempton, R.A. and Taylor, L.R. (1976). “Models and statistics for species diversity”. Nature (262): 818-820._
- **Lladser’s confidence interval**: Calculates Lladser’s confidence interval
  - Single confidence interval of the conditional uncovered probability
  - **`--p-metric`: lladser_ci**
  - _Lladser, M.E., Gouet, R., Reeder, R. (2011). “Extrapolation of Urn Models via Poissonization: Accurate Measurements of the Microbial Unknown”. PLoS._
- **Lladser’s point estimate**: Calculates Lladser’ point estimate
  - Estimates how much of the environment contains unsampled taxa
  - Best estimate on a complete sample
  - **`--p-metric`: lladser_pe**
  - _Lladser, M.E., Gouet, R., Reeder, J. (2011). “Extrapolation of Urn Models via Poissonization: Accurate Measurements of the Microbial Unknown”. PLoS._
- **Margalef’s richness index**: Calculates Margalef’s richness index
  - Measures species richness in a given area or community
  - **`--p-metric`: margalef**
  - _Magurran, A.E. (2004). “Measuring biological diversity”. Blackwell. 76-77._
- **Mcintosh dominance index D**: Calculates McIntosh dominance index D
  - Affected by the variation in dominant taxa and less affected by the variation in less abundant or rare taxa
  - **`--p-metric`: msintosh_d**
  - _McIntosh, R.P. (1967). “An index of diversity and the relation of certain concepts to diversity”. Ecology (48): 392-404._
- **Mcintosh evenness index E**: Calculates McIntosh’s evenness measure E
  - How evenly abundant taxa are
  - **`--p-metric`: mcintosh_e**
  - _Heip, C. (1974). “A new index measuring evenness”. J. Mar. Biol. Ass. UK. (54) 555-557._
- **Menhinick’s richness index**: Calculates Menhinick’s richness index
  - The ratio of the number of taxa to the square root of the sample size
  - **`--p-metric`: menhinick**
  - _Magurran, A.E. (2004). “Measuring biological diversity”. Blackwell. 76-77._
- **Michaelis-Menten fit to rarefaction curve of observed OTUs**: Calculates Michaelis-Menten fit to rarefaction curve of observed OTUs.
  - Estimated richness of species pools
  - **`--p-metric`: michaelis_mentin_fit**
  - _Raaijmakers, J.G.W. (1987). “Statistical analysis of the Michaelis-Menten equation”. Biometrics. (43): 793-803._
- **Number of distinct features**: Calculates number of distinct OTUs
  - **`--p-metric`: observed_otus**
  - _DeSantis, T.Z., Hugenholtz, P., Larsen, N., Rojas, M., Brodie, E.L., Keller, K. Huber, T., Davis, D., Hu, P., Andersen, G.L. (2006). “Greengenes, a Chimera-Checked 16S rRNA Gene Database and Workbench Compatible with ARB”. Applied and Environmental Microbiology (72): 5069–5072._
- **Number of double occurrences**: Calculates number of double occurrence OTUs (doubletons)
  - OTUs that only occur twice
  - **`--p-metric`: doubles**
- **Number of observed features, including singles and doubles**: Calculates number of observed OTUs, singles, and doubles.
  - **`--p-metric`: osd**
  - _DeSantis, T.Z., Hugenholtz, P., Larsen, N., Rojas, M., Brodie, E.L., Keller, K. Huber, T., Davis, D., Hu, P., Andersen, G.L. (2006). “Greengenes, a Chimera-Checked 16S rRNA Gene Database and Workbench Compatible with ARB”. Applied and Environmental Microbiology. 72 (7): 5069–5072._
- **Singles**: Calculates number of single occurrence OTUs (singletons)
  - OTUs that appear only once in a given sample
  - **`--p-metric`: singles**
- **Pielou’s evenness**: Calculates Pielou’s eveness
  - Measure of relative evenness of species richness
  - **`--p-metric`: pielou_e**
  - _Pielou, E. (1966). “The measurement of diversity in different types of biological collections”. J. Theor. Biol. (13): 131-144._
- **Robbins’ estimator**: Calculates Robbins’ estimator
  - Probability of unobserved outcomes
  - **`--p-metric`: robbins**
  - _Robbins, H.E. (1968). “Estimating the Total Probability of the unobserved outcomes of an experiment”. Ann Math. Statist. 39(1): 256-257._
- **Shannon’s index**: Calculates Shannon’s index
  - Calculates richness and diversity using a natural logarithm
  - Accounts for both abundance and evenness of the taxa present
  - **`--p-metric`: shannon**
  - _Shannon, C.E. and Weaver, W. (1949). “The mathematical theory of communication”. University of Illonois Press, Champaign, Illonois._
- **Simpson evenness measure E**: Calculates Simpson’s evenness measure E.
  - Diversity that account for the number of organisms and number of species
  - **`--p-metric`: simpson_e**
  - _Simpson, E.H. (1949). “Measurement of Diversity”. Nature. (163): 688_
- **Simpson’s index**: Calculates Simpson’s index
  - Measures the relative abundance of the different species making up the sample richness
  - **`--p-metric`: simpson**
  - _Simpson, E.H. (1949). “Measurement of diversity". Nature. (163): 688._
- **Strong’s dominance index (Dw)**: Calculates Strong’s dominance index
  - Measures species abundance unevenness
  - **`--p-metric`: strong**
  - _Strong, W.L. (2002). “Assessing species abundance uneveness within and between plant communities”. Community Ecology (3): 237-246._

## Beta Diversity Analysis

The `beta` and `beta-phylogenetic` methods compute a user-specified beta diversity metric for all samples in a feature table.

Phylogenetic beta diversity metrics (in this case, Unweighted UniFrac), can be run with the following command:

```bash
qiime diversity beta-phylogenetic \
  --i-table table.qza \
  --i-phylogeny rooted-tree.qza \
 --p-metric unweighted_unifrac \
 --o-distance-matrix unweighted_unifrac_distance_matrix.qza
```

Non-phylogenetic beta diversity metrics (in this case, Bray-Curtis), can be run with the following command:

```bash
qiime diversity beta \
  --i-table table.qza \
 --p-metric braycurtis \
 --o-distance-matrix unweighted_unifrac_distance_matrix.qza
```

The `--i-table` input provides the feature table containing the samples for which the beta diversity metric will be computed. The `--i-phylogeny` input provides the phylogenetic tree containing the tip identifiers that correspond to the feature identifiers in the table, and is only used for the `beta-phylogenetic` command (i.e., when computing phylogenetic diversity metrics. The `--p-metric` parameter specifies the beta diversity metric to be run. The ` --o-distance-matrix` output specifies the output file.

To compute a different beta diversity metric, change the ``--p-metric` parameter to the one that corresponds to the metric you want to compute. The following list provides information on the available beta diversity metrics in QIIME 2.

- **Bray-Curtis dissimilarity**: Calculates Bray–Curtis dissimilarity
  - Fraction of overabundant counts
  - **`--p-metric`: braycurtis**
  - _Sorenson, T. (1948) "A method of establishing groups of equal amplitude in plant sociology based on similarity of species content." Kongelige Danske Videnskabernes Selskab 5.1-34: 4-7._
- **Canberra distance**: Calculates Canberra distance
  - Overabundance on a feature by feature basis
  - **`--p-metric`: canberra**
  - _Lance, Godfrey L.N. and Williams, W.T. (1967). "A general theory of classificatory sorting strategies II. Clustering systems." The computer journal 10 (3):271-277._
- **Chebyshev distance**: Calculates Chebyshev distance
  - Maximum distance between two samples
  - **`--p-metric`: chebyshev**
  - _Cyrus. D. Cantrell (2000). “Modern Mathematical Methods for Physicists and Engineers”. Cambridge University Press._
- **City-block distance**: Calculates City-block distance
  - Similar to the Euclidean distance but the effect of a large difference in a single dimension is reduced
  - **`--p-metric`: cityblock**
  - _Paul, E.B. (2006). “Manhattan distance". Dictionary of Algorithms and Data Structures_
- **Correlation coefficient**: Measures Correlation coefficient
  - Measure of strength and direction of linear relationship between samples
  - **`--p-metric`: correlation**
  - _Galton, F. (1877). "Typical laws of heredity". Nature. 15 (388): 492–495._
- **Cosine Similarity**: Measures Cosine similarity
  - Ratio of the amount of common species in a sample to the mean of the two samples
  - **`--p-metric`: cosine**
  - _Ochiai, A. (1957). “Zoogeographical Studies on the Soleoid Fishes Found in Japan and its Neighhouring Regions-II”. Nippon Suisan Gakkaishi. 22(9): 526-530._
- **Dice measures**: Calculates Dice measure
  - Statistic used for comparing the similarity of two samples
  - Only counts true positives once
  - **`--p-metric`: dice**
  - _Dice, Lee R. (1945). "Measures of the Amount of Ecologic Association Between Species". Ecology. 26 (3): 297–302._
- **Euclidean distance**: Measures Euclidean distance
  - Species-by-species distance matrix
  - **`--p-metric`: euclidean**
  - _Legendre, P. and Caceres, M. (2013). “Beta diversity as the variance of community data: dissimilarity coefficients and partitioning.” Ecology Letters. 16(8): 951-963._
- **Generalized Unifrac**: Measures Generalized UniFrac
  - Detects a wider range of biological changes compared to unweighted and weighted UniFrac
  - **`--p-metric`: generalized_unifrac**
  - _Chen, F., Bittinger, K., Charlson, E.S., Hoffmann, C., Lewis, J., Wu, G. D., Collman, R.G., Bushman, R.D., Li,H. (2012). “Associating microbiome composition with environmental covariates using generalized UniFrac distances.” Bioinformatics. 28 (16): 2106-2113._
- **Hamming distance**: Measures Hamming distance
  - Minimum number of substitutions required to change one group to the other
  - **`--p-metric`: hamming**
  - _Hamming, R.W. (1950) “Error Detecting and Error Connecting Codes”. The Bell System Technical Journal. (29): 147-160._
- **Jaccard similarity index**: Calculates Jaccard similarity index
  - Fraction of unique features, regardless of abundance
  - **`--p-metric`: jaccard**
  - _Jaccard, P. (1908). “Nouvellesrecherches sur la distribution florale.” Bull. Soc. V and. Sci. Nat., (44):223-270._
- **Kulczynski dissimilarity index**: Measures Kulczynski dissimilarity index
  - Describes the dissimilarity between two samples
  - **`--p-metric`: kulsinski**
  - _Kulcynski, S. (1927). “Die Pflanzenassoziationen der Pieninen. Bulletin International de l’Academie Polonaise des Sciences et des Lettres”. Classe des Sciences Mathematiques et Naturelles. 57-203._
- **Mahalanobis distance**: Calculates Mahalanobis distance
  - How many standard deviations one sample is away from the mean
  - Unitless and scale-invariant
  - Takes into account the correlations of the data set
  - **`--p-metric`: mahalanobis**
  - _Citation: Mahalanobis, Chandra, P. (1936). "On the generalised distance in statistics". Proceedings of the National Institute of Sciences of India. 2 (1): 49–55._
- **Matching components**: Measures Matching components
  - Compares indices under all possible situations
  - **`--p-metric`: matching**
  - _Janson, S., and Vegelius, J. (1981). “Measures of ecological association”. Oecologia. (49): 371–376._
- **Rogers-tanimoto distance**: Measures Rogers-Tanimoto distance
  - Allows the possibility of two samples, which are quite different from each other, to both be similar to a third
  - **`--p-metric`: rogerstanimoto**
  - _Tanimoto, T. (1958). "An Elementary Mathematical theory of Classification and Prediction". New York: Internal IBM Technical Report._
- **Russel-Rao coefficient**: Calculates Russell-Rao coefficients
  - Equal weight is given to matches and non-matches
  - **`--p-metric`: russelrao**
  - _Russell, P.F. and Rao, T.R. (1940). “On habitat and association of species of anopheline larvae in south-eastern Madras”. J. Malaria Inst. India. (3): 153-178._
- **Sokal-Michener coefficient**: Measures Sokal-Michener coefficient
  - Proportion of matches between samples
  - **`--p-metric`: sokalmichener**
  - _Sokal, R.R. and Michener, C.D. (1958). “A statistical method for evaluating systematic relationships”. Univ. Kans. Sci. Bull. (38) 1409-1438._
- **Sokal-Sneath Index**: Calculates Sokal-Sneath index
  - Measure of species turnover
  - **`--p-metric`: sokalsneath**
  - _Sokal, R.R. and Sneath, P.H.A. (1963). “Principles of Numerical Taxonomy”. W. H. Freeman, San Francisco, California._
- **Species-by-species Euclidean**: Measures Species-by-species Euclidean
  - Standardized Euclidean distance between two groups
  - Each coordinate difference between observations is scaled by dividing by the corresponding element of the standard deviation
  - **`--p-metric`: seuclidean**
  - _Legendre, P. and Caceres, M. (2013). “Beta diversity as the variance of community data: dissimilarity coefficients and partitioning.” Ecology Letters. 16(8): 951-963._
- **Squared Euclidean**: Measures squared Euclidean distance
  - Place progressively greater weight on samples that are farther apart
  - **`--p-metric`: sqeuclidean**
  - _Legendre, P. and Caceres, M. (2013). “Beta diversity as the variance of community data: dissimilarity coefficients and partitioning.” Ecology Letters. 16(8): 951-963._
- **Unweighted unifrac**: Measures unweighted UniFrac
  - Measures the fraction of unique branch length
  - **`--p-metric`: unweighted_unifrac**
  - _Lozupone, C. and Knight, R. (2005). "UniFrac: a new phylogenetic method for comparing microbial communities." Applied and environmental microbiology 71 (12): 8228-8235._
- **Weighted Minkowski metric**: Measures Weighted Minkowski metric
  - Allows the use of the k-means-type paradigm to cluster large data sets
  - **`--p-metric`: wminkowski**
  - _Chan, Y., Ching, W.K., Ng, M.K., Huang, J.Z. (2004). “An optimization algorithm for clustering using weighted dissimilarity measures”. Pattern Recognition. 37(5): 943-952._
- **Weighted normalized UniFrac**: Measures Weighted normalized UniFrac
  - Takes into account abundance
  - Normalization adjusts for varying root-to-tip distances.
  - **`--p-metric`: weighted_normalized_unifrac**
  - _Lozupone, C. A., Hamady, M., Kelley, S. T., Knight, R. (2007). "Quantitative and qualitative beta diversity measures lead to different insights into factors that structure microbial communities". Applied and Environmental Microbiology. 73(5): 1576–85._
- **Weighted unnormalized UniFrac**: Measures Weighted unnormalized UniFrac
  - Takes into account abundance
  - Doesn't correct for unequal sampling effort or different evolutionary rates between taxa
  - **`--p-metric`: weighted_unifrac**
  - _Lozupone, C. A., Hamady, M., Kelley, S. T., Knight, R. (2007). "Quantitative and qualitative beta diversity measures lead to different insights into factors that structure microbial communities". Applied and Environmental Microbiology. 73(5): 1576–85._
- **Yule index**: Measures Yule index
  - Measures biodiversity
  - Determined by the diversity of species and the proportions between the abundance of those species.
  - **`--p-metric`: yule**
  - _Fisher, R.A., Corbert, A.S., Williams, C.B. (1943). “The Relationship Between the Number of Species and the Number of Individuals in a Random Sample of an Animal Population”. J. Animal Ecol. (12): 42-58._

To further analyze the results of your beta and alpha diversities, return to the [QIIME 2 “Moving Pictures Tutorial”](https://docs.qiime2.org/2017.11/tutorials/moving-pictures/) tutorial and continue at the “alpha-group-significance” command.
