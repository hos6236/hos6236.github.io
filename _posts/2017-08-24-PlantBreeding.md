---
layout: post
title: Plant Breeding and Molecular Marker
---

## Concepts in Plant Breeding
- Important breeding concepts

- Survey plant breeding methods

- Best Linear Mixed Effect

- Pedigree and relationship	matrices

- Breeding value prediction and BLUP

- Random x fixed Effects

### Slides

1. [Breeding concepts](https://github.com/lfelipe-ferrao/lfelipe-ferrao.github.io/blob/master/classes/plant_breeding_1.pdf)

2. [Plant breeding methods](https://github.com/lfelipe-ferrao/lfelipe-ferrao.github.io/blob/master/classes/plant_breeding_2.pdf)

3. [Breeding value prediction and BLUP](https://github.com/lfelipe-ferrao/lfelipe-ferrao.github.io/blob/master/classes/plant_breeding_3.pdf)

## Concepts in DNA Molecular Markers

- Morphologival Markers

- Hybridization- Based Markers

- Whole Genome Sequencing

- Sequence Capture

- Genotype by Sequencing (GBS)

- SNP chips

### Slides

1. [Molecular Markers](https://github.com/lfelipe-ferrao/lfelipe-ferrao.github.io/blob/master/classes/plant_breeding_4.pdf)

## R codes

### Introduction

```
######################################################
######     I. R As a calculator    ####################
######################################################

# Sum
7 + 3   #I can comment or annotate my scripts by writing after the # sign

# Divide
9 / 3

# Square Root
9 ^ (1/2)
9 ^ 1 /2  ## what happens?
sqrt(9)   ## build in function in R

# Logaritm
log(10) #natural logarith default
log(10,base = 10)
log10(10)
log(10,base = 2)

# exponentials
exp(1)
exp(2)

# arithmetic calculation #
ceiling (67 / 3) # the most closest integer larger than the result
floor(67 / 3) # the most closest integer smaller than the result

#########NEED HELP ##########
?sqrt
?log
#############################


######################################################
######     II.R creating objects    ####################
######################################################

## Naming Variables ##
dice = c(1,2,3,4,5,6)
dice  = c(1,2,3,4,5,6) =

b = c(1, 3, 5, 7)                    		# assign a vector to the object
b
c = list(x = c(4, 2, 6), y = c(3, 6, 1))    # assign a list to the object
c
e = matrix(seq(from = 2, to = 17, by = 1), 4, 4)   # assign a matrix to the object
e
z = rnorm(n = 16, mean = 2, sd = 3)                  # assign a vector, which can be used in the   following lines
f = data.frame(x = seq(1:16), y = rep(1,16), z)    # assign a data.frame to the object
f

# R is case sensitive #
MEAN(z)
mean(z)

## Function within a function

log (x = sqrt(9))
log(3)

## basic stats

numbers = c(10.5,2.0,8.7,6,4.5,7)

mean(numbers)
sum(numbers)
cumsum(numbers)
sd(numbers)

# Matrices

?matrix
my.matr = matrix(data = numbers,nrow = 2, ncol = 2)
dim(my.matr)                            # show the dimension of the matrix
str(my.matr)

matrix(c(1:10), nrow = 5)               # the functions rank the elements after column in default
matrix(c(1:10), nrow = 5, byrow = TRUE) # argument byrow changes the ranking sequence by row

# matrix operation

my.matrix = matrix(rnorm(n = 16, mean = 10, sd = 4), nrow = 4); my.matrix
t(my.matrix)                            # transpose matrix
solve(my.matrix)                        # inverse a square matrix

matrix.data = matrix(1:16, nrow = 4); matrix.data
matrix.data * matrix.data               # element-wise multiplication
matrix.data %*% matrix.data             # Matrix multiplication
diag(1:16, nrow = 16)                   # create a diagonal matrix with elements in the principal diagonal
diag(matrix.data)                       # what if we put a matrix in the argument?

colSums(matrix.data)                    # get the sum of columns
rowSums(matrix.data)                    # get the sum of rows

# Lists
my.list = list(my.matrix = matrix(c(1:20),ncol = 5),
                my.vetor = c(1:20),
                fruts = c("banana", "orange","grapes"))

my.list$my.matrix
my.list$my.vetor
my.list$fruts

# data.frame
df = data.frame(a = rpois(100, 20), b = 1:100, c = rnorm(100, 20, 5), d = rep(1:2, 50))
df
head(df)                                 # just show the first 6 rows
tail(df)

# generate a vector from normal distribution

n_dis = rnorm(n=10,m=1,sd=0.3)
hist(n_dis)
plot(density(n_dis))

n_dis = rnorm(n = 10, m = 1, sd = 0.3)
plot(density(n_dis))

n_dis = rnorm(n = 100, m = 1, sd = 0.3)
plot(density(n_dis))

n_dis = rnorm(n= 1000, m = 1, sd = 0.3)
plot(density(n_dis))

n_dis = rnorm(n = 10000, m = 1, sd = 0.3)
plot(density(n_dis))

n_dis = rnorm(n = 100000, m = 1, sd = 0.3)
plot(density(n_dis))


######################################################
######     III. Characters    #######################
######################################################

# character combination

colors = c("red", "blue", "purple", "yellow")
colors
more.colors = c("pink", "black")
collect.colors = c(colors, more.colors) # characters and characters put together are still character
collect.colors
mix.up = c(colors, c(1, 2))             # the numeric elements are coerced to be characters
mix.up

# string manipulation

grep("cat", c("xcat", "fat cat", "slim cat", "carpet", "cat")) # check the match for "cat" in the vector
grep("Cat", c("xcat", "fat cat", "slim cat", "carpet", "cat")) # case sensitive
collection = c("xcat", "fat cat", "slim cat", "carpet", "cat"); collection
position = grep("cat", c("xcat", "fat cat", "slim cat", "carpet", "cat")); position
collection[position]

nchar(collection)         # length of a string (space is a string character as well)

substr(collection, start = 1, stop = 4) # get the letters start from position 1 to 4

paste(collection, "is funny", sep = "") # directly paste elements together
paste(collection, "is funny", sep = " ")# connect with  a space

temp = paste(collection, "is", collection, sep = " "); temp # can put multiple elements together
length(temp)                            # see how many elements in the vector
temp2 = paste(collection, "is", collection, collapse = " "); temp2
length(temp2)                           # the whole vector collapse into one element
nchar(temp2)                            # check the length of the string character

i = 10
test = sprintf("the the cubic square of %d is %d", i, i ^ 3)  # print into a string
test

strsplit("2-29-2015", split = "-")      # split the strings by the later "-" string

test2 = paste(seq(from = 1, to = 12, by = 1), seq(from = 1, to = 30, by = 1), seq(from = 2015, to = 2044, by = 1), sep = "-")
test2
split.test2 = strsplit(test2, split = "-"); split.test2  # what will happen if we run this line
length(split.test2[[1]])                # within each sublist, there are three strings

regexpr("at", "density of fat in a rat")# find the first matching pattern position

gregexpr("at", "density of fat in a rat")# find all instances of the pattern


#######################################################
######     IV. Logic operations #######################
#######################################################

3 > 4                                    # Boolean value: TRUE or FALSE

numbers = c(10.5, 2.0, 8.7, 6, 4.5, 7)
numbers[3] == 3                           # check whether the thrid element of the vector is equal to 3 or not
numbers[3]                                # confirm the result
numbers > 2


select = which(numbers > 2); select # which (x = "condition tested")
numbers[select]

Letters = c("a", "b", "c", "r", "a")
which(Letters == "a")                    # can be used on vectors of characters as well

Letters[5]
Letters[which(Letters == "a")]         # select all the "a" elements from the vector

#######################################################################################
######     V. OPENING AND SAVING FILES - USIGN EXTERNAL DATA    #######################
#######################################################################################



# opening and saving a file

getwd()
setwd("/Users/marcio/OneDrive - University of Florida/HOS 6236 - 2017/HOS 6236/Fall 2017/Week 2") ##fill with your path to archives
read.table("opening_file.txt")
read.table("opening_file.txt",header = T)
read.table("opening_file.txt",header = T,check.names = F)
read.table("opening_file.txt",header = T,check.names = F,row.names = 1)
read.table("opening_file.txt",header = T,check.names = F,row.names = 1,na.strings = -9)
read.table("opening_file.csv")
read.table("opening_file.csv",header = T,check.names = F,row.names = 1,na.strings = -9,sep = ",")

help(read.csv)

my.new.file = as.matrix(read.table("opening_file.csv",header = T,check.names = F,row.names = 1,na.strings = -9,sep = ","))

my.new.file[c(1,2,4)] = 100
which(my.new.file == 2)
my.new.file[which(my.new.file == 2)] = 100

write.table(x = my.new.file, file = "new_file.txt", row.names = T, col.names = T, quote = F)

############################
#    Example 1             #
############################

	SNPraw = as.matrix(read.csv("SNPdata_samplePine_Raw.csv",row.names = 1,na.string = "NA"))

	dim(SNPraw)
	SNPraw[1:10,1:10]
	table(SNPraw[,1])

	source("ConvertGenotypes.R")
	SNPready = Convert_SNPdata(SNPfile = "SNPdata_samplePine_Raw.csv",missingValue = NA,keepMono = TRUE)

	table(SNPready[,1])
	table(SNPready[,2])

     n0 = apply(SNPready ==0,2,sum,na.rm=T)
     n1 = apply(SNPready ==1,2,sum,na.rm=T)
     n2 = apply(SNPready ==2,2,sum,na.rm=T)

     n = n0 + n1 + n2

     ## calculate allele frequencies
     p = ((2*n0)+n1)/(2*n)
     q = 1 - p
     maf = pmin(p, q)

	filt1.SNPready = SNPready[,-which(n==0)]
	filt2.SNPready = SNPready[,-which(maf<0.05)]
	filt3.SNPready = SNPready[,-which(maf<0.05 | n==0)]
############################
#    Example 2             #
############################

	Phenotype = as.matrix(read.csv("phenotype_example.csv",row.names = 1))
	head(Phenotype)
	plot(Phenotype)
	plot(density(Phenotype))
	hist(Phenotype,nclass=100)
	summary(Phenotype)


##########################################################
######     VI. HIGH-LEVEL PLOTS    #######################
##########################################################

# barplot
barplot(VADeaths, beside = TRUE, legend = TRUE, ylim = c(0,90),
        ylab = "Deaths per 1000", main = "Death Rates in Virginia")  

# Pie Chart
groupsize = c(15, 35, 32, 6, 6, 6)
labels = c("A", "B", "C", "D", "E", "F")
pie(groupsize, labels, main = "Pie chart for Field Plot Technique") # you can define the colors by coding

# Histograms

x = rnorm(n = 10000, mean = 30, sd = 5)
hist(x)
hist(x, breaks = 20)
hist(x, breaks = "Scott")
hist(x, breaks = "Freedman-Diaconis")  # different number of bins

# Box plots
head(iris)
boxplot(Sepal.Length ~ Species, data = iris, ylab = "Sepal length", main = "Iris measurements", boxwex = 0.8)

# Scatterplot

x = rnorm(1000)
y = rpois(1000, 20)
mean(y)                                # confirm the mean of the data

plot(x, y, main = "Poisson vs. Normal")
plot(x, y, main = "Poisson vs. Normal", type = "l")
plot(sort(x), sort(y), type = "l")

```
