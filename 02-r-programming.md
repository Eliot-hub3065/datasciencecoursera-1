# R Programming

https://www.coursera.org/course/rprog

* dialect of S, from bell labs in the 70's. open sourced in 93
* bioconductor.org biological data analysis

## Types

* atomic classes: character, numeric (double precision real), integer (suffix with L), complex, logical (T/F)
* vector must has same type
* list can be mixed type
* Inf, NaN, NA (nullish value, `is.na`, `is.nan`)
* implicit coercion if mix types in vectors
* explicit coercion `as.numeric|character|logical|complex`

## Objects

* attributes: names, dimname (dimension name), class, length, user defined
* `class(x)` to display type
* `unclass(x)` to strip the type and see underlying representation

## Matrices

* vector with a `dimension` attribute `matrix(nrow=2, ncol=3)`. Use `dim` to add dimension attribute to an existing vector.
* constructed column-wise: `matrix(1:6, nrow=2, ncol=3)`
* `cbind`, `rbind` create matrix via vectors

## Factors

* categories: unordered: male / female, ordered: student, phd, postdoc
* self describing, better than enum of integers
* `factor(c("yes", "yes", "no", "yes"), levels=c("yes", "no"))`
* `table(f)` to count by levels

## Data frames

* tabular data. special type of list
* matrix has same type, but data frame can be mixed. `data.matrix` coerces
* `row.names`
* usually create with `read.table`, `read.csv`
* `data.frame(foo = 1:4, bar = c(T,T,F,F))`

## Names

* user defined attributes on objects
* `names(v)` to view on vector
* `names(v) <- c('a', 'b', 'c')` to define on vector
* `list(a=1, b=2)`
* `dimnames(m) <- list(c('row1', 'row2'), c('col1', 'col2'))` on matrix

## Reading data

```r
# tabular data
read.table  # sep=" "
write.table
read.csv    # sep=",", header=T

read.table(
  file='',
  header=T,
  sep=',',
  colClasses=c("numeric", "numeric"), # faster than inferring from data
  stringsAsFactors=T,
  nrows=100,
  comment.char = "",  # faster without comments
)

# optimization: set colClasses
small <- read.table("db.txt", nrows=100)
classes <- sapply(small, class) # classes from a small set
read.table("db.txt", colClasses = classes)

# text file
readLines / writeLines

# R files
source / dget / dput

# workspace
load

# marshaling objects
unserialize / save, serialize

# Connections
con <- file("foo.txt", "r")
gzfile
bzfile
url

# alternative to reading by path
data <- read.csv(con)
close(con)
```

## Subsetting

```r
x <- c("a", "b", "c", "c", "d", "a")

# extracts the same type as the original object
x[1]       # "a" subset by numeric index
x[1:4]     # "a" "b" "c" "c" subset by range
x[x > "a"] # "b" "c" "c" "d" subset by conditional
u < x > "a"
x[u]       # same as above, subset by logicals


# extracts element, but not the same type

# extract named element, not necessarily of the same type
```
