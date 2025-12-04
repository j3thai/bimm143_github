# Class 6: R functions
Jennifer Thai (PID: A17893762)

All functions in R have at least 3 things:

- A **name**, we pick this and use it to call the function.
- Input **arguments**, there can be multiple comma separated inputs to
  the function.
- The **body**, lines of R code that do the work of the function.

Our first wee function:

``` r
add <- function(x, y=1) {
  x + y
}
```

Let’s test our function

``` r
add(c(1,2,3), y=10)
```

    [1] 11 12 13

``` r
add(10)
```

    [1] 11

``` r
add(10, 10)
```

    [1] 20

## A second function

Let’s try something more interesting. Make a sequence generation tool.

The `sample()` function could be useufl here.

``` r
sample(1:10, size=3)
```

    [1]  1  2 10

Change this to work with the nucleotides A, C, G, and T, and return 3 of
them

``` r
n <- c("A", "C", "G", "T")
sample(n, size=15, replace=TRUE)
```

     [1] "A" "A" "T" "T" "A" "T" "A" "A" "G" "C" "C" "C" "T" "G" "A"

Turn this snippet into a function that returns a user specified length
DNA sequence. Let’s call it `generate_dna()`…

``` r
generate_dna <- function(len=10, fasta=FALSE) {
  n <- c("A", "C", "G", "T")
  v <- sample(n, size=len, replace=TRUE)
  
  # Make a single element vector 
  s <- paste(v, collapse="")
  
  cat("Well done you!\n")
  
  if(fasta) {
    return( s )
  } else {
    return ( v )
  }
}
```

``` r
generate_dna(5)
```

    Well done you!

    [1] "G" "G" "G" "G" "T"

``` r
s <- generate_dna(15)
```

    Well done you!

``` r
s
```

     [1] "T" "C" "C" "G" "A" "A" "C" "A" "C" "C" "C" "C" "T" "T" "G"

I want the option to return a single element character vector with my
sequence all together like this: “GGAGTAC”

``` r
generate_dna(10, fasta=TRUE)
```

    Well done you!

    [1] "TCAAAGCGAA"

``` r
generate_dna(10, fasta=FALSE)
```

    Well done you!

     [1] "T" "A" "A" "G" "C" "A" "A" "T" "T" "G"

## A more advanced example

Make a third function that generates protein sequence of a user
specified length and format.

``` r
a <- c("A", "R", "N", "D", "C", "Q", "E", "G", "H", "I", "L", "K", "M", "F", "P", "S", "T", "W", "Y", "V")
sample(a, size=15, replace=TRUE)
```

     [1] "Y" "S" "D" "K" "R" "G" "F" "P" "F" "H" "F" "T" "V" "N" "L"

``` r
generate_protein <- function(len=10, fasta=TRUE) {
  a <- c("A", "R", "N", "D", "C", "Q", "E", "G", "H", "I", "L", "K", "M", "F", "P", "S", "T", "W", "Y", "V")
  seq <- sample(a, size=len, replace=TRUE)
  
  p <- paste(seq, collapse="")
  
  if(fasta) {
    return( p )
  } else {
    return ( seq )
  }
}
```

``` r
generate_protein(10)
```

    [1] "TVDEHKEHIA"

> Q. Generate random protein sequences between lengths 5 and 12 amino
> acids.

``` r
generate_protein(5)
```

    [1] "DNCTH"

``` r
generate_protein(6)
```

    [1] "IRDPVA"

One approach is to do this by brute force calling our function for each
length 5 to 12.

Another approach is to write a `for()` loop to iterate over the input
valued 5 to 12.

A very useful third R specific approach is to use the `sapply()`
function.

``` r
seq_lengths <- 5:12
for (i in seq_lengths) {
  cat(">", i, "\n", sep="")
  cat( generate_protein(i) )
  cat("\n")
}
```

    >5
    KDVNK
    >6
    DHRNAH
    >7
    HMTHIWI
    >8
    VEYWCSFD
    >9
    DAITKPAFL
    >10
    TEHPAMLQLC
    >11
    LPINEMIPTDN
    >12
    TTDGNTDDRFGK

``` r
sapply(5:12, generate_protein)
```

    [1] "WYCIG"        "TWHYFL"       "YDKQYAY"      "TSGGNYNI"     "QRYCNCTFW"   
    [6] "MWVSEEGCGN"   "TWIVNYVRVHE"  "AHNLNMKLPAFM"

> **Key Point**: Writing functions in R is doable but not the easiest
> thing. Starting with a working snippet of code and then using LLM
> tools to improve and generalize your function is a productive
> approach.
