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

## R/qtl package

by ``Luis Felipe V. Ferrão``

 In this section, we pointed out four  QTL mapping methods implemented in the ``R/qtl`` package. They have been widely used in the last decade in animal, plant and human research.  Exception the Single Marker Analysis approach, all interval mapping methods require the prior establishment of a linkage genetic map (linking the concepts discussed in the last class about the importance of linkage mapping).

 In this [link](https://github.com/hos6236/hos6236.github.io/blob/master/classes/QTLmapping_2.pdf) is possible to access a short ``R/qtl`` tutorial created by Ivone de Bem Oliveira. Please, use this material as a reference to guide you in the exercises. If you want to get more in deep into this topic, be sure to access the material signed by **Karl Bromam**. He is an active researcher in this area and in this [link](http://www.rqtl.org/) it is possible to have information about complete tutorials, books and discussion groups on the subject. In the author's [github page](https://github.com/kbroman) there are further information.

Below, a brief report about the methods discussed in class.

### Single Marker Analysis

The simplest method for the analysis of QTL mapping data is to consider each marker individually, split the individuals into groups, according to their
genotypes at the marker, and compare the groups’ phenotype averages.

Advantages:
1. The key advantage of marker regression is its simplicity: we just perform a t test or ANOVA at each marker.
2. No special software is required (``lm`` function in R can be used).
3. Does not need a previous linkage genetic map.
4. Can be applied to non-linked markers.
5. Theoretical basis of the genome-wide association studies (GWAS).

Disadvantages:
1. Cannot inspect positions between markers.
2. Poor information about QTL location.
3. Model single QTL, which does not allow for more complex models including epistasis or other interactions.

### Standard (or Simple) Interval Mapping (IM)

SIM method allows systematically go through the genome in search of QTLs. Statistically, it is an extension of the analysis of each single marker, allowing analysis at intervals. The computational and statistical implementation proposed by [Haley and Knott (1992)](http://www.nature.com/hdy/journal/v69/n4/abs/hdy1992131a.html?foxtrotcallback=true) and [Martinez and Curnow (1992)](https://link.springer.com/article/10.1007/BF00222330), at the same year, became popular in the literature since they described a fast approximation of the ordinary least square (OLS) method for mapping QTLs.

Advantages:
1. Inference about the QTL position.
2. Increase of the statistical power.

Disadvantages:
1. Excludes effects of other QTLs for the tested region, so it can result in false positives (called "ghosts" QTL).
2. Not use all genome information in the analyzes.

### Composite Interval Mapping (CIM)

 So far, it was presented only single-QTL models:  we hypothesized the presence of a single QTL in each position in the genome, one at a time, as the location of that QTL. The model can be improved including a nearby typed marker as a covariate in further analysis, in order to reduce the residual variation and so improve our ability to detect further QTL. Statistically, single regression models become multiple regression models, by the inclusion of other markers in the model as covariates. This is the most popular QTL mapping approach and it was widely used in animal, plant and human research.

 Advantages:

 1. Reduce residual variation and so give increased power to detect QTL.
 2. use all genome information in the analysis.

 Disadvantages:

 1. Inefficient to model more complex scenarios considering interaction effects.

### Multiple Interval Mapping (MIM)

All previous methods have considered the follow question: "Is there a QTL here ?". For this, single marker analysis considered  each marker individually, the SIM method considered a similar regression model but considering prior linkage mapping information and CIM approach fitted a multiple regression model assuming neighboring markers as covariates. An alternative question is:“Are there QTL here and here?”. This is the idea behind of the MIM method.Simply stating, MIM is a method that simultaneously considers multiples QTLs. For this purpose, multiple procedures to compare and select models are necessary. As pointed out by K. Broman: "QTL mapping is best viewed as a model selection or variable selection problem: what set of loci (and QTL × QTL interactions) are best supported by the data? ".

 Advantages:
1. Combines high precision and statistical power
2. Inclusion of epistasis and other interactions sources in the model.
3. Better description of the genetic architecture of a quantitative trait.
4. Estimate the number, position, effects and interaction between QTLs.

### Toy example

Below is presented the ``R/qtl`` codes discussed during the class. Some important points:

-  In ``R/qtl`` book, the MIM method is pointed out as a powerful approach. Given the time, we'll focus on the CIM method (the most popular in the literature).

- Download the data set using this [link.](http://www.rqtl.org/sug.csv)

- Permutation argument (``n.perm``) in the ``cim`` and ``scanone`` function performe a permutation test to get a significance threshold. Here, we are assuming a tiny number of permutation given the time. In a real analysis, you should increase it.

- QTL effects is an important information. In the  ``R/qtl`` book, the author pointed out: "The function for performing QTL mapping, ``scanone``, does not provide estimated QTL effects. Such estimates are best obtained with the function ``fitqtl()``, particularly for the case of a multiple QTL model". A solution to get this effects in the CIM analysis was proposed by Karl Broman at the `R/qtl` discussion group. He pointed out:  "We don't have a way to get effect estimates or phenotypic variance explained except through the ``fitqtl()`` function. Once you've decided on some set of QTL, use ``makeqtl()`` to create a ``qtl object`` and then ``fitqtl()`` with ``get.ests=TRUE`` to get estimated effects and estimated percent variance explained." In this toy example, we will consider this alternative to get the QTL effects.



```
#######################   R CODES  #####################
require('qtl')

# 1) IMPORTING TYHE DATA
# -- Data from Sugiyama et al., Physiol Genomics 10:5–12, 2002.
# -- Row 1: names of phenotypes + markers
# -- Row 2: No. chromosomes (genetic map)
# -- Row 3: Position in the chr (genetic map)
# -- Row 3+n: phenotypic value +  genotype

original.dataset = read.csv("/home/lfelipe/Dropbox/PosDoc_UF/HOS6236_MolecularMarkersPlantaBreeding/qtl_toyExample/sug.csv")
original.dataset[1:10,1:10] #subset

# Importing in the R/QTL package
sug	<-	read.cross("csv",	"/home/lfelipe/Dropbox/PosDoc_UF/HOS6236_MolecularMarkersPlantaBreeding/qtl_toyExample/",
                  "sug.csv", 	
                  genotypes=c("CC",	"CB",	"BB"),	alleles=c("C",	"B"))
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
qtl.im = summary(IM.hk,threshold = 3) # QTL threshold > 3
plot(IM.hk, col = "red", ylab = "LOD Score")
abline(h = 3, lty = 2)

# -------- ## -------- ## -------- #

# 3) COMPOSITE INTERVAL MAPPING
# -- Multiple linear regression,considering a grid of positions along the genome
# -- Markers as covariates (reduce residual variation and increase the power)
set.seed(123)
CIM = cim(hyper, pheno.col = 3, n.marcovar=5, window=20)
qtl.cim = summary(CIM,threshold = 3)
cov.position = attr(CIM, "marker.covar.pos") #covariates position
plot(IM.hk, col = "blue", ylab = "LOD Score")
abline(h = 3, lty = 2)

# -------- ## -------- ## -------- #

# 4) COMPARING IM x CIM | PERMUTATION
chr <- c(1:19)
plot(IM.hk, CIM, chr = chr, col = c("blue", "red"), ylab = "LOD Score")
add.cim.covar(CIM, chr = chr, col = "darkgreen")
abline(h = 2, lty = 2, col="black") # naive threshold

set.seed(123)
cim.perm = cim(hyper, pheno.col = 3, n.marcovar=5, window=20,n.perm = 10)
summary(cim.perm)
abline(h = summary(cim.perm)[1], lty = 2) # threshold using permutation

# -------- ## -------- ## -------- #

# 5) QTL effect
# -- Comparing the results
qtl.im.make = makeqtl(hyper, chr = qtl.im$chr,pos=qtl.im$pos,what="prob")
qtl.eff.im = fitqtl(hyper,qtl=qtl.im.make,method="hk",get.ests=TRUE, dropone=FALSE)
summary(qtl.eff.im)

qtl.cim.make = makeqtl(hyper, chr = cov.position$chr,pos=cov.position$pos,what="prob")
qtl.eff.cim = fitqtl(hyper,qtl=qtl.cim.make,method="hk",get.ests=TRUE, dropone=FALSE)
summary(qtl.eff.cim)



```
