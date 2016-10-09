---
title: "Scala Cheat Sheet"
description: "Scala Cheat Sheet"
category: Programming
tags: [programming]
sidebar:
  nav: "new_side"
---

Inspired by [Scalacheat](http://docs.scala-lang.org/cheatsheets/)

# Table of contents

* TOC
{:toc}

# Preliminaries
```scala
```

(<a href="#top">Back to top</a>)
<hr>



# Variables
```scala
val x = 5  #GOOD 
x=6  # BAD 	constant
var x: Double = 5	 # explicit type
```

(<a href="#top">Back to top</a>)
<hr>

# Control structures


# Functions

```scala
// hidden error: without = it’s a Unit-returning procedure; causes havoc
def f(x: Int) = { x*x } 

// varargs.
def sum(args: Int*) = args.reduceLeft(_+_)	
```

(<a href="#top">Back to top</a>)
<hr>

## Call-by-name vs call-by-value
```scala
def f(x: R)  # call-by-value 
def f(x: => R)	# call-by-name (lazy parameters)
```

(<a href="#top">Back to top</a>)
<hr>


## Anonymous function
```scala
(x:R) => x*x

// underscore is positionally matched arg.
1 to 5).map(_*2) vs. (1 to 5).reduceLeft( _+_ )

// block style returns last expression.
(1 to 5).map { x => val y=x*2; println(y); y }	

// pipeline style. (or parens too).
(1 to 5) filter {_%2 == 0} map {_*2}
```

(<a href="#top">Back to top</a>)
<hr>


## Currying
```scala
// obvious syntax.
val zscore = (mean:R, sd:R) => (x:R) => (x-mean)/sd
// obvious syntax
def zscore(mean:R, sd:R) = (x:R) => (x-mean)/sd
// sugar syntax. but then:
def zscore(mean:R, sd:R)(x:R) = (x-mean)/sd
```

(<a href="#top">Back to top</a>)
<hr>

# Packages

# Import
```scala
// wildcard import
import scala.collection._	

// selective import
import scala.collection.Vector 
import scala.collection.{Vector, Sequence}	

// renaming import.
import scala.collection.{Vector => Vec28}	

// import all from java.util except Date.
import java.util.{Date => _, _}	
```

# Declare
```scala
// declare a package.
package pkg { ... }	
```

(<a href="#top">Back to top</a>)
<hr>

# Input / Output

## Read

### CSV
```scala
```

(<a href="#top">Back to top</a>)
<hr>


### Generate Testdata

(<a href="#top">Back to top</a>)
<hr>

## Write

### File
```R
```

(<a href="#top">Back to top</a>)
<hr>

(<a href="#top">Back to top</a>)
<hr>




# Data Structures
(<a href="#top">Back to top</a>)
<hr>

