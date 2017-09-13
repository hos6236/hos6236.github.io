---
layout: post
title: Linkage Mapping
---

 "In 1909, the only time during his twenty–four years at Columbia, 
Morgan gave the opening lectures in the undergraduate course in
beginning zoology. It so happened that C. B. Bridges and I were both
in the class. While genetics was not mentioned, we were both
attracted to Morgan and were fortunate enough, though both still
undergraduates, to be given desks in his laboratory the following year
(1910–1911).The possibilities of the genetic study of Drosophila
were then just beginning to be apparent; we were at the right place at
the right time. … In the latter part of 1911, in conversation with
Morgan … I suddenly realized that the variations in strength of
linkage, already attributed by Morgan to differences in the spatial
separation of the genes, offered the possibility of determining
sequences in the linear dimension of a chromosome. I went home and
spent most of the night (to the neglect of my undergraduate
homework) in producing the first chromosome map, which included
the sex–linked genes y, w, v, m, and r, in the order and approximately
the relative spacing that they still appear on the standard maps"

`Sturtevant, 1913`

-------------------------------------------


## Concepts

- What are linkage maps?

- Mapping populations.

- Identification of polymorphism.

- Linkage analysis of markers.

- Genetic distance and mapping functions.

### Slides

1. [Linkage mapping introduction](https://github.com/lfelipe-ferrao/lfelipe-ferrao.github.io/blob/master/classes/linkage_mapping_1.pdf)

2. [Linkage mapping construction](https://github.com/lfelipe-ferrao/lfelipe-ferrao.github.io/blob/master/classes/linkage_mapping_3.pdf)

3. [Chi-squared test and a toy example of Mendelian segregation distortion ](https://github.com/lfelipe-ferrao/lfelipe-ferrao.github.io/blob/master/classes/linkage_mapping_2.pdf)

## Onemap

``OneMap`` is a software for constructing genetic maps in experimental crosses: full-sib, RILs, F2 and backcrosses. This [github page](https://github.com/augusto-garcia/onemap) has its version under development. New functions will be added (experimental work) and, once it is done, we will synchronize the repositories and add it to CRAN. The complete tutorial to build a linkage map for inbred-based populations (F2, RIL and BC) and for outcrossing populations can be accessed by these links ([F2 population](http://augustogarcia.me/onemap/vignettes_highres/Inbred_Based_Populations.html#combining-onemap-objects) and [outcrossing](http://augustogarcia.me/onemap/vignettes_highres/Outcrossing_Populations.html)). Please, check these tutorials. They have described the main concepts necessary to build a linkage map. A reduced version based on these tutorials was prepared by Ivone de Bem Oliveira and can be accessed using this link ([reduced version](https://github.com/lfelipe-ferrao/lfelipe-ferrao.github.io/blob/master/classes/linkage_mapping_4.pdf))

## Project (by Ivone de Bem Oliveira)

Files for the first project can be downloaded [here](https://github.com/lfelipe-ferrao/lfelipe-ferrao.github.io/blob/master/classes/linkage_mapping_exer.zip).

Description:

- ``f2_report1.raw`` = Data file already in OneMap format.

- ``LG_students.csv`` = Each student has been assigned a set of LG that should analyzed for his/her project.

- ``Rubric_Lab1_OneMap.doc`` = This is the basic expectation for your report, including the weight on the final score for each portion.

- ``OneMap_tutorial_Aug2017`` = This is the step-by-step tutorial with all what we covered in class today plus extra steps you may need to complete your project.

Please pay attention because the data for the project comes from an F2 population. The tutorial was done for an outcrossing population, however, the functions are almost the same. You can also found another tutorial for F2 populations in the links provided in the tutorial.

For this specific report you are not required to perform the distortion test. Also, use LOD=4, the recombination fraction=0.5 and the mapping function is Kosambi. You can explore other options, but as a minimum you need to use the above parameters for the main project.

The due date, given the hurricane Irma, has been extended by Friday 15 by 5 PM. Please email back to me the report as a pdf file.

Ivone de Bem Oliveira
