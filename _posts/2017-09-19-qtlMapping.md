---
layout: post
title: QTL Mapping
---

  "Apart from sex linkage, we know almost nothing at present of linkage in man. Yet it is certain that every defect determined by a single factor must be located in one or other of twenty-three linkage groups. Each defect must therefore be linked in inheritance with numerous other observable traits, and with some of them is probably linked closely. The search for such linkage will certainly be lengthy, and at first, disappointing."

`Sir Ronald Fisher`-  Eugenics, academic and practical. Eugenics Review, 27, 95-100, 1935

-------------------------------------------

## Concepts

- QTL definition.

- Linkage disequilibrium.

- Single Marker Regression.

- Interval Mapping.

- Composite Inverval Mapping (CIM).

- Permutation.

## Slides

1. [Introduction to QTL analysis.](https://github.com/hos6236/hos6236.github.io/blob/master/classes/QTLmapping_1.pdf)

2. [Permutation test and more about QTL analysis.](https://github.com/hos6236/hos6236.github.io/blob/master/classes/QTLmapping_5.pdf)

## R/qtl package

by ``Luis Felipe V. Ferrão``

 In this section, we pointed out four  QTL mapping methods implemented in the ``R/qtl`` package. They have been widely used in the last decade in animal, plant, and human research.  With the exception of the Single Marker Analysis approach, all interval mapping methods presented require the prior establishment of a linkage genetic map (linking the concepts discussed in the last class about the importance of linkage mapping).

 In this [link](https://github.com/hos6236/hos6236.github.io/blob/master/classes/QTLmapping_2.pdf) it is possible to access a short ``R/qtl`` tutorial created by Ivone de Bem Oliveira. If you want to learn more about this topic, be sure to access the material by **Karl Broman**. He is an active researcher in this area and in this [link](http://www.rqtl.org/) it is possible to have information about complete tutorials, books and discussion groups on the subject. In the author's [github page](https://github.com/kbroman) there is further information.

Below, a brief report about the methods discussed in class.

### Single Marker Analysis

The simplest method for the analysis of QTLs is to consider each marker individually and independently from each other,  split the individuals into groups, according to their genotypes at the marker, and compare the groups’ phenotype averages.

Advantages:
1. The key advantage of marker regression is its simplicity: we just perform a t test or ANOVA at each marker.
2. No special software is required (``lm`` function in R can be used).
3. Does not require a previous linkage genetic map.
4. Can be applied to non-linked markers.
5. Theoretical basis of the genome-wide association studies (GWAS).

Disadvantages:
1. Cannot inspect positions between markers.
2. Poor information about QTL location.
3. Model single QTL, which does not allow for more complex models including epistasis or other interactions.

### Standard (or Simple) Interval Mapping (IM)

The IM method allows systematically exploration of the genome in search of QTLs. Statistically, it is an extension of the analysis of each single marker, allowing analysis at intervals of markers across the linkage groups. The computational and statistical implementation proposed by [Haley and Knott (1992)](http://www.nature.com/hdy/journal/v69/n4/abs/hdy1992131a.html?foxtrotcallback=true) and [Martinez and Curnow (1992)](https://link.springer.com/article/10.1007/BF00222330), at the same year, became popular in the literature since they described a fast approximation of the ordinary least square (OLS) method.

Advantages:
1. Better inference about the QTL position.
2. Increase of the statistical power.

Disadvantages:
1. Excludes effects of other QTLs linked to the region being tested, so it can result in false positives (called "ghosts" QTL).
2. Does not use all the genome information in the analyzes simultaneously.

### Composite Interval Mapping (CIM)

 So far, all methods above search for single-QTL:  we hypothesized the presence of a single QTL in each position in the genome, one at a time. The model can be improved including a nearby marker as a covariate in further analysis, in order to reduce the residual variation and so improve our ability to detect QTL. Statistically, single regression models become multiple regression models, by the inclusion of other markers in the model as covariates. CIM is the most popular QTL mapping approach and has been widely used in animal, plant and human research.

 Advantages:

 1. Reduce residual variation and so give increased power to detect QTL.
 2. Uses all genome information in the analysis.

 Disadvantages:

 1. Inefficient to model more complex scenarios considering interaction effects.

### Multiple Interval Mapping (MIM)

At this point, some comments are necessary. All previous methods have considered the follow question: "Is there a QTL linked to this marker or interval?". For this, the first approach (single marker analysis) considered  each marker individually, without previous information about linkage groups. The IM method uses a similar regression model but considering prior linkage mapping information to fit the model. Finally, the CIM approach fitted a multiple regression model assuming other molecular markers as covariates in the regression model.

An alternative question is:“Are there QTL here and there?”. This is the idea behind of the MIM method. Briefly, MIM is a method that simultaneously considers multiples QTLs. For this purpose, multiple procedures to compare and select models are necessary. As pointed out by K. Broman: "QTL mapping is best viewed as a model selection or variable selection problem: what set of loci (and QTL × QTL interactions) are best supported by the data? ". Modern studies of QTL mapping have been based in this theory

 Advantages:
1. Combines high precision and statistical power
2. Inclusion of epistasis and other interactions sources in the model.
3. Better description of the genetic architecture of a quantitative trait.
4. Estimate the number, position, effects and interaction between QTLs.

### Demo (a toy example)

Below is presented the ``R/qtl`` code discussed during the class. Some important points:

-  MIM method was pointed out as a powerful approach. However, given the short time during class, we'll focus on the CIM method, the most popular in the literature. In [Ivone's tutorial](https://github.com/hos6236/hos6236.github.io/blob/master/classes/QTLmapping_2.pdf) and on the [Karl Broman's page](http://www.rqtl.org/) there are various details about the MIM approach.  

- [Data set used in this example](https://github.com/hos6236/hos6236.github.io/blob/master/classes/QTLmapping_6.csv).

- Permutation argument (``n.perm``) in the ``cim`` and ``scanone`` function performs a permutation test to get a significance threshold to call markers linked to QTLs. Here, we are assuming a small number of permutations given the short time. In a real analysis, you run at least 1000 to determine the treshold. .

- **The QTL effect is important information.** In the  ``R/qtl`` book, the author pointed out: "The function for performing QTL mapping, ``scanone``, does not provide estimated QTL effects. Such estimates are best obtained with the function ``fitqtl()``, particularly for the case of a multiple QTL model". A solution to get this effects in the CIM analysis was proposed by Karl Broman in the `R/qtl` discussion group in a topic addressing "how to obtain the QTL effects and other information in CIM analysis?". He pointed out:  "We don't have a way to get effect estimates or phenotypic variance explained except through the ``fitqtl()`` function. Once you've decided on some set of QTL, use ``makeqtl()`` to create a ``qtl object`` and then ``fitqtl()`` with ``get.ests=TRUE`` to get estimated effects and estimated percent variance explained." In this toy example, we will consider this alternative to get the QTL effects.

- [Original paper.](https://github.com/hos6236/hos6236.github.io/blob/master/classes/QTLmapping_3.pdf)

```
############################    R CODES   ############################

require('qtl') 	

# 1) IMPORTING THE DATA
# -- Data from Sugiyama et al., Physiol Genomics 10:5–12, 2002.
# -- Row 1: names of phenotypes + markers
# -- Row 2: No. chromosomes (genetic map)
# -- Row 3: Position in the chr (genetic map)
# -- Row 3+n: phenotypic value +  genotype

original.dataset = read.csv("/home/lfelipe/Dropbox/PosDoc_UF/HOS6236_MolecularMarkersPlantaBreeding/qtl_toyExample/sug.csv")
original.dataset[1:10,1:10] #subset

# Importing in the R/QTL package
sug	<-	read.cross("csv","/home/lfelipe/Dropbox/PosDoc_UF/HOS6236_MolecularMarkersPlantaBreeding/qtl_toyExample/","sug.csv",genotypes=c("CC",	"CB",	"BB"),	alleles=c("C",	"B"))
summary(sug)
plot(sug)

# -------- ## -------- ## -------- #

# 2) SINGLE MARKER REGRESSION  (homework)
mr <- scanone(sug, pheno.col=3,method="mr")
plot(mr, ylab="LOD score")
summary(mr,threshold = 3)
par(mfrow=c(1,2)) # compare the groups’ phenotype averages
plot.pxg(sug, "D15MIT184")
plot.pxg(sug, "D1MIT171")

# -------- ## -------- ## -------- #

# 3) INTERVAL MAPPING
# -- Simple linear regression,considering a grid of positions along the genome
hyper = calc.genoprob(sug,step=1) # cond. prob

IM.hk = scanone(hyper, pheno.col = 3, method = "hk") #Pheno=3 (bw trait)
head(IM.hk) #LOD for each position of the linkage mapping ("sweeping the genome")
qtl.im = summary(IM.hk,threshold = 2.5) # QTL threshold > 2.5 (naive threshold)
qtl.im

plot(IM.hk, col = "red", ylab = "LOD Score")
abline(h = 2.5, lty = 2)

# -------- ## -------- ## -------- #

# 3) COMPOSITE INTERVAL MAPPING
# -- Multiple linear regression,considering a grid of positions along the genome
# -- Markers as covariates (reduce residual variation and increase the power)
set.seed(123)
CIM = cim(hyper, pheno.col = 3, n.marcovar=5, window=20)
head(CIM) #LOD for each position of the linkage mapping ("sweeping the genome")
qtl.cim = summary(CIM,threshold = 2.5) # QTL threshold > 2.5 (naive threshold)
qtl.cim

plot(CIM, col = "blue", ylab = "LOD Score")
abline(h = 2.5, lty = 2)

# -------- ## -------- ## -------- #

# 4) COMPARING IM x CIM
# -- Problems to use a naive threshold (?)
# -- QTLs common across the methods (?)
# -- QTLs different across the methods (?)
# -- Difference in magnitude of the peaks (?)
# -- Increase the window size or the number of covariates (?)
# -- Is there a right answer (?)

chr <- c(1:19)
plot(IM.hk, CIM, chr = chr, col = c("blue", "red"), ylab = "LOD Score")
add.cim.covar(CIM, chr = chr, col = "darkgreen")
abline(h = 2.5, lty = 2, col="black") # naive threshold

# -------- ## -------- ## -------- #

# 5) PERMUTATION TEST
# -- Let's be more formal (!)
set.seed(123)
cim.perm = cim(hyper, pheno.col = 3, n.marcovar=5, window=20,n.perm = 10)
summary(cim.perm)
abline(h = summary(cim.perm)[1], lty = 2, col= "green") # threshold using permutation

# -------- ## -------- ## -------- #

# 5) QTL EFFECTS
# -- Compare the results effects
# -- Difference in the phenotype variation explained (?)
# -- Difference in the effects and SE (?)

# IM method
qtl.im = summary(IM.hk,threshold = summary(cim.perm)[1])
qtl.im # selected QTL using the IM and permutation test
qtl.im.make = makeqtl(hyper, chr = qtl.im$chr,pos=qtl.im$pos,what="prob")
qtl.eff.im = fitqtl(hyper,qtl=qtl.im.make,method="hk",get.ests=TRUE, dropone=FALSE)
summary(qtl.eff.im)

# CIM method
qtl.cim = summary(CIM,threshold = summary(cim.perm)[1])
qtl.cim # selected QTL using the CIM and permutation test
cov.position = attr(CIM, "marker.covar.pos")
cov.position # covariates position
qtl.cim.make = makeqtl(hyper, chr = cov.position$chr,pos=cov.position$pos,what="prob")
qtl.eff.cim = fitqtl(hyper,qtl=qtl.cim.make,method="hk",get.ests=TRUE, dropone=FALSE)
summary(qtl.eff.cim)

```

------------
# QTL project

- Deadline:  Thursday, September 28 at 5 pm. 

The main objective of this project is to map QTLs comparing the three methods discussed during the class (Single Marker Regression, Interval Mapping and Composite Interval Method). The data set is the same as that we have used during the class. You can download it using this [link](https://github.com/hos6236/hos6236.github.io/blob/master/classes/QTLmapping_6.csv). In this link you can click at the ``raw`` icon at the right corner of the page, copy the data, save in ``.csv`` format, and import to the ``R``. 

After install the ``R/qtl`` package, another alternative is to use the follow function in the ``R`` console: ``sug <- read.cross("csv", "http://www.rqtl.org", "sug.csv",genotypes=c("CC", "CB", "BB"), alleles=c("C", "B"))`` . The ``read.cross`` function is from the ``R/qtl`` package and it is able to download the data directly from the website. This function can fail if the web page is not working.  

During the lesson, we mapped QTLs for the ``bw`` trait (it was not used in the original paper for QTL mapping puorposes). The original data set contains other three phenotypes (``hr``, ``bp`` and ``heart_wt``).  **Each student has been assigned a trait that should analyzed for his/her project.**  In this [link](https://github.com/hos6236/hos6236.github.io/blob/master/classes/QTLmapping_4.csv) you can see the trait assigned to you. If you intend to use the codes showed during the class, make sure to change the argument ``pheno.col=3`` in the ``scanone`` or ``cim`` functions. This argument controls the trait considered in the QTL analysis.

The reason to consider this dataset is due to the amount of information available. This data set was extensively discussed in the literature and on the  ``R/qtl`` page there are good tutorials. You should take this information to familiarize yourself with the methods. Visit the ``R/qtl`` discussion group is always an important source of knowledge.

## Contents

### Introduction (2pt)

- An introduction about the importance to consider QTL mapping in plant breeding studies -300 to 600 words.

### QTL mapping (6 pt)

- A brief description about the objectives of the [original paper](https://github.com/hos6236/hos6236.github.io/blob/master/classes/QTLmapping_3.pdf) and the data set considered (number of markers, population size and type, phenotype considered and other information) (2pt).

- Describe the QTLs identified considering the methods: Single Marker Regression, Interval Mapping and Composite Interval Method.  Indicate the QTL position in the linkage group, their effects, and other relevant information. Use graphics to represent the results for each method (4 pts).

### Conclusion (2 pt)

- Interpret the results. You can focus your interpretation on the additive effects estimated by the Composite Interval Method (CIM), which was discussed during the class. In addition, you should highlight differences and similarities across the methods and compare your results with the findings observed in the original paper. Finally, you can use this section to discuss alternative methods not reported in the original paper or during the classes (1 pt).

- In a plant breeding scenario. If you were a breeder and this example is a real breeding population, how would you propose to use QTL information? (1 pt)

Luis Felipe V. Ferrão (lfelipe.ferrao@gmail.com)
