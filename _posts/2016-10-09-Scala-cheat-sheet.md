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

## template body
```scala
object HelloWorld extends App {
  println("Hello, World!")
}
```

with arguments 

```scala
object HelloWorld {
  def main(args: Array[String]) {
    println("Hello, World!")
  }
}
```

(<a href="#top">Back to top</a>)
<hr>



# Variables
```scala
var x = 1  // mutableval x = 1  // immutableval s = “foo”  // implicit typeval i:Int = 1  // explicit type
```

(<a href="#top">Back to top</a>)
<hr>

# Control structures

## if
```scala
// conditional. 
if (check) happy else sad	

// equivalent 
if (check) happy 
if (check) happy else ()

// if else 
if (x >= 0) x else -x
```

## while
```scala
while (x < 5) { println(x); x += 1}

// do while
do { println(x); x += 1} while (x < 5)

// break
import scala.util.control.Breaks._
breakable {
	for (x <- xs) {
		if (Math.random < 0.1) break
		}
	}
```

## for
```scala
// iterate including the upper bound
for (i <- 1 to 5) {
	println(i)
}	

// iterate omitting the upper bound
for (i <- 1 until 5) {
	println(i)
}

// for (not a loop, but expression)
val xs = Seq(1, 2, 3)
for (x <- xs) println(x)
// <- binds x to each element of collection xs, is a generator 

// iterate files
for (  file <- files  if file.isFile  if file.getName.endsWith(“.a”)) doSomething(file)

// for comprehension: filter/map
for (x <- xs if x%2 == 0) yield x*10 
// same as 
xs.filter(_%2 == 0).map(_*10)	

// destructuring bind
for ((x,y) <- xs zip ys) yield x*y 
// same as 
(xs zip ys) map { case (x,y) => x*y }	

// cross product
for (x <- xs; y <- ys) yield x*y 
// same as 
xs flatMap {x => ys map {y => x*y}}	

// imperative-ish: sprintf-style
for (x <- xs; y <- ys) {
	println("%d/%d = %.1f".format(x,y, x*y))
}	
```

## Iterators
```scala
// Map | Dictionary
val m = Map(1 -> "a", 2 -> "b", 3 -> "c")
for ((pos, letter) <- m) println("the letter '"+letter+"' has the "+pos+". position in the alphabet")

 // List
val doubleValues = for (x <- (1 to 5).toList) yield x*2
// yield only in for, only must appear at most once 

 // Range
val doubleValues = for (i <- (0 until xs.length)) yield xs(i)*2
 // get evenValues
val evenValues = for (x <- (0 to 10) if x%2 == 0) yield x
 // if is here a filter, doesn't need ()

// Collections: 2 collections simultaneously 
val arr = Array(Array(1, 2, 3),Array(4, 5, 6),Array(7, 8, 9))
val values = for (x <- (1 to 3); y <- (1 to 3); z = x*y if z%2 == 0) yield z


// class elements
for (x <- x1.productIterator) println(x)

// command line arguments
args.foreach(arg => println(arg))args.foreach(println(_))args.foreach(println)
```

## Recursion
```scala
def loop(i: Int): String =
  if (i <= 9) i+loop(i+1) else ""
```

### Tail recursion

* tail recursion
* doesn't know about status of other recursion steps
* GOOD: optimizer can optimize to loop + easiness of recursion writing
* final variable will be added as further parameter

```scala
import scala.annotation.tailrec
@tailrec def loop(i: Int, s: String): String =
    if (i <= 9) loop(i+1, s+i) else s  

```

## Try, catch, finally
```scala
try {  something} catch {  case ex: IOException => // handle  case ex: FileNotFoundException =>    // handle} finally { doStuff }
```


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
(x: Int) => x + 1

// with multiple parameters
(x: Int, y: Int) => "(" + x + ", " + y + ")"

// no parameters
() => { System.getProperty("user.dir") }

// underscore is positionally matched arg.
1 to 5).map(_*2) vs. (1 to 5).reduceLeft( _+_ )

// block style returns last expression.
(1 to 5).map { x => val y=x*2; println(y); y }	

// pipeline style. (or parens too).
(1 to 5) filter {_%2 == 0} map {_*2}
```

(<a href="#top">Back to top</a>)
<hr>

## Nested functions - local scope
```scala
// useful: piece of code with local scope (don't want global)
def str: String = {
  def loop(i: Int, s: String): String =
    if (i <= 9) loop(i+1, s+i) else s
  loop(0, "")
}
// only method str is visible    
```


## Currying
Methods may define multiple parameter lists. When a method is called with a fewer number of parameter lists, then this will yield a function taking the missing parameter lists as its arguments.

```scala
object CurryTest extends App {
  def filter(xs: List[Int], p: Int => Boolean): List[Int] =
    if (xs.isEmpty) xs
    else if (p(xs.head)) xs.head :: filter(xs.tail, p)
    else filter(xs.tail, p)
  def modN(n: Int)(x: Int) = ((x % n) == 0)
  val nums = List(1, 2, 3, 4, 5, 6, 7, 8)
  println(filter(nums, modN(2)))
  println(filter(nums, modN(3)))
}

// Output
List(2,4,6,8)
List(3,6)
```

(<a href="#top">Back to top</a>)
<hr>

# Pattern matching
```scala
// use case in function args for pattern matching.
(xs zip ys) map { case (x,y) => x*y }

// “v42” is interpreted as a name matching any Int value, and “42” is printed.
// BAD
val v42 = 42
Some(3) match {
	case Some(v42) => println("42")
	case _ => println("Not 42")
}	

// ”`v42`” with backticks is interpreted as the existing val v42, and “Not 42” is printed.
// GOOD
val v42 = 42
Some(3) match {
	case Some(`v42`) => println("42")
	case _ => println("Not 42")
}	
// UppercaseVal is treated as an existing val, rather than a new pattern variable, because it starts with an uppercase letter. Thus, the value contained within UppercaseVal is checked against 3, and “Not 42” is printed.
// GOOD
val UppercaseVal = 42
Some(3) match {
	case Some(UppercaseVal) => println("42")
	case _ => println("Not 42")
}	
```

(<a href="#top">Back to top</a>)
<hr>

# Object orientation

## Constructor

```scala
// constructor params: private
class C(x: R) 
// same as 
class C(private val x: R)
// access
var c = new C(4)	

// constructor params - public
class C(val x: R)
// access
var c = new C(4)
c.x	
```

```scala
// constructor is class body
class C(var x: R) {
	assert(x > 0, "positive please")
	var y = x  // declare a public member
	val readonly = 5  // declare a private member
	private var secret = 1
	def this = this(42)
}
	alternative constructor
```

### Scope
```scala
// public (default) and private
class A {
  private def x = ...
  def y = ...
}
//A.y works, but A.x doesn't
```

(<a href="#top">Back to top</a>)
<hr>

## Abstract class
```scala
// abstract -> can't create object
// define an abstract class. (non-createable)
abstract class D { ... }	
```

(<a href="#top">Back to top</a>)
<hr>

## Inheritance
```scala
// define an inherited class.
class C extends D { ... }	

// inheritance and constructor params. (wishlist: automatically pass-up params by default)
class D(var x: R)
class C(x: R) extends D(x)	

// e.g.
class Manager(name: String, age: Int) extends Person(name, age)
```

### Force implementation
```scala
// force inherited class to have implementation. override keyword to method name
abstract class Printable {
       override def toString: String
}
```

### Scope
```scala
//protected, only within declared and inherited scope 
class A {
  protected def x = ...
}
class B extends A {
  // x is accessible
}
```


### Example
```scala
// abstract -> can't create object
// abstract class has unprecise behaviour
abstract class Person {
  def sayHello() { println("hello") }
  def doWork() // is also abstract --> needs implementation
}
class Manager extends Person {
  def doWork() { println("rake in money") }
}
class Programmer extends Person {
  def doWork() { println("write code") }
}
```

(<a href="#top">Back to top</a>)
<hr>

## Superclass

### Access

```scala
// access variable of superclass via this-keyword
this.c = c
// access method of superclass
super.x
```

## Overriding
```scala
// avoid override --> final keyword
class Tester {
        final def isValid(i: Int) = i < 5
}
// --> forbids method override
final class Tester
// --> forbids class extension
```

## Singleton
Methods and values that aren’t associated with individual instances of a class belong in singleton objects, denoted by using the keyword object instead of class.

```scala
package test
object Blah {
  def sum(l: List[Int]): Int = l.sum
}```

(<a href="#top">Back to top</a>)
<hr>

## Traits
Similar to interfaces in Java, traits are used to define object types by specifying the signature of the supported methods. Like in Java 8, Scala allows traits to be partially implemented; i.e. it is possible to define default implementations for some methods. In contrast to classes, traits may not have constructor parameters
traits like class except. [source](http://docs.scala-lang.org/tutorials/tour/traits)

```scala
//  This trait consists of two methods isSimilar and isNotSimilar. While isSimilar does not provide a concrete method implementation (it is abstract in the terminology of Java), method isNotSimilar defines a concrete implementation

trait Similarity {
  def isSimilar(x: Any): Boolean   // does not provides concrete method implementation
  def isNotSimilar(x: Any): Boolean = !isSimilar(x) // provides concrete method implementation
}

// Consequently, classes that integrate this trait only have to provide a concrete implementation for isSimilar
class Point(xc: Int, yc: Int) extends Similarity {
  var x: Int = xc
  var y: Int = yc
  def isSimilar(obj: Any) =
    obj.isInstanceOf[Point] &&
    obj.asInstanceOf[Point].x == x
}

object TraitsTest extends App {
  val p1 = new Point(2, 3)
  val p2 = new Point(2, 4)
  val p3 = new Point(3, 3)
  println(p1.isNotSimilar(p2))
  println(p1.isNotSimilar(p3))
  println(p1.isNotSimilar(2))
}

// multiple traits.
trait T1; trait T2
class C extends T1 with T2
class C extends D with T1 with T2	
```

(<a href="#top">Back to top</a>)
<hr>


## Checks
```scala
// 	class literal.
classOf[String]

// type check (runtime)
x.isInstanceOf[String]	

// type cast (runtime)
x.asInstanceOf[String]	

// ascription (compile time)
x: String	
```

## Case classes
```scala
// keyword 'case' 
case class Address(city: String, zip: Int, street: String)
case class Person(name: String, age: Int, address: Address)
// named arguments
case class X(i: Int, s: String)

// copy case class
val x1 = X(8, "hello")


// extractor
val p = Person("franz", 43, Address("gornau", 12345, "rabenweg"))

// extract p
val Person(name, age, address @ Address(city, zip, street)) = p
```

(<a href="#top">Back to top</a>)
<hr>

# Packages

## Import
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

(<a href="#top">Back to top</a>)
<hr>

## Declare
```scala
// declare a package.
package pkg { ... }	
```

(<a href="#top">Back to top</a>)
<hr>

# Input / Output

## Read

### File
```scala
import scala.io.Source;
val reader = Source.fromFile("test.txt")
for (line <- reader.getLines()){
	println(line)
}

// reading lines
//1000002 1 55
 val (id, name) = line.span(_ != '\t')
      if (name.isEmpty) {
        None
      } else {
        try {
          Some((id.toInt, name.trim))
        } catch {
          case e: NumberFormatException => None
        }
      }

```

### CSV
```scala
```

(<a href="#top">Back to top</a>)
<hr>


### Generate Testdata

(<a href="#top">Back to top</a>)
<hr>

## Write

### Command line
```scala
println(s"Hello, $name")
println(f"$name%s is $height%2.2f meters tall")
```

### File
```scala
val file = new File(canonicalFilename)
val bw = new BufferedWriter(new FileWriter(file))
bw.write(text)
bw.close()

// or
import java.io.PrintWriter;
val writer = new PrintWriter("")
writer.write("")
writer.close()
```

(<a href="#top">Back to top</a>)
<hr>

(<a href="#top">Back to top</a>)
<hr>




# Data Structures
### OVERVIEW OF DATA STRUCTURES + INHERITANCE
![{{base}}/images/lambda_architecture.png]({{base}}/images/programming/Scala-class-hierarchy.gif)

[image source](https://github.com/mbonaci/scala/blob/master/resources/Scala-class-hierarchy.gif?raw=true)


## String

```scala
val string = args.mkString(" ")
```

### replace
```scala
input.replaceAll("""(?m)\s+$""", "")
```

(<a href="#top">Back to top</a>)
<hr>

## Collections

### constructors
```scala
// Seq
val xs = Seq[Int](1,2,3)
val str: Seq[Char] = "8735421960" // string == val str = "8735421960"

// LIST
val xs = List(1, 2, 3)
val xs = 1 :: 2 :: 3 :: Nil 
// Nil is singleton object
// "::" concats elements

//IndexedSeq (Vector + Array)
// Vector immutable, Array mutable.
// Vector is based on Array (with immutable flag set)
// constructors
val xs = IndexedSeq(1, 2, 3) // gives Vector by default
val xs = Array(1, 2, 3)

//RANGE
// to
1 to 5 // 1.to(5)  // to is method
// until (exclusive last value)
1 until 5
// with method "by"
1 to 10 by 2 // Range(1, 3, 5, 7, 9)
10 to 1 by -2 // Range(10, 8, 6, 4, 2)
```

(<a href="#top">Back to top</a>)
<hr>

### Methods 
```scala
// size
xs.size

//Access
xs(0)
xs.contains(1) // true || false
xs.head // first element
xs.last // last element
xs.tail // all but first
xs.init // all but last
```

(<a href="#top">Back to top</a>)
<hr>

#### add element 

```scala
// (to end)
xs :+ 4
xs :+= 4 // assign to xs
// (to beginning)
4 +: xs
// add another list (to)
xs ++ Seq(4, 5, 6)
xs = Seq[Int](1,2,3) // assign to xs
xs.++(List(4, 5, 6)) // add to end (O(n))
xs.:::(List(4, 5, 6)) // add to beginning (is cheaper (O(1)))
```

#### Delete
```scala
x.drop(2) // drops first 2 elements
```

(<a href="#top">Back to top</a>)
<hr>

#### Iterators
```scala
//Iterator (lazy evaluators)
// method "iterator" returns iterator
//  can be traversed only once! 
//  knows only 1 element at a time
val i = xs.iterator
while(i.hasNext) // if there is a next
    println(i.next) // i++
```

(<a href="#top">Back to top</a>)
<hr>

#### Print
```scala
println(xs.mkString("[", ", ", "]"))
```

(<a href="#top">Back to top</a>)
<hr>

//View
// is own collection. 
// Can be traversed multiple times
// creates a new collection for every operation. can run "drop" multiple times
val v = xs.view

//Stream
// allows creation of infinite long collections
// ?? not sure

(<a href="#top">Back to top</a>)
<hr>

## Set, Tuple, Map
* Set
	*  not sorted
* Tuple
 	* any kind of data the will be "linked"
 	*  is not a collection
 	*  idea: passing around related data
* Map
	* key-value pairs

### constructor
```scala
 // Set
val set = Set(1, 2, 3)

// Tuple
("de", "Germany") 
(1, "hello", 5.34)
1 -> "hello"
(1).->("hello") // 2 tuple
 
 // map
val m = Map("de" -> "Germany", "en" -> "England", "fr" -> "France")

(<a href="#top">Back to top</a>)
<hr>

### Access
```scala
 // tuple
res130._1

// map
m("de")
m.get("de")
```

(<a href="#top">Back to top</a>)
<hr>


### Functions
```scala
 // map
m.keys
m.values

//exists

(<a href="#top">Back to top</a>)
<hr>

### add 
```scala
//  add List to set --> gives only unique elements
set ++ List(3, 4, 5)
// convert seq to set!
val set = Set() ++ xs
```

(<a href="#top">Back to top</a>)
<hr>

### sort
```scala
import scala.collection.immutable.SortedSet
// append list to new SortedSet
// needs to be specificed a type manually
val set = SortedSet[Int]() ++ xs
```

(<a href="#top">Back to top</a>)
<hr>

### Iterator
```scala
    // tuple
    val t = (6, "hello", 3.245, true, 'h')
    val i = t.productIterator
    while (i.hasNext) println(i.next)
```

(<a href="#top">Back to top</a>)
<hr>

# Math

## functions
```scala
// absolute value
 (-1).abs

// safely dividing by zero
def something(x: Int, y: Int) = Try(x/y).getOrElse(0)
```

(<a href="#top">Back to top</a>)
<hr>

# Advances

## Actors
Actors are the core elements that make Scala scalable. Actors act as coroutines, managing the underlying threads pool. Actors communicate through passing asynchronous messages.
[link](http://www.scala-lang.org/old/node/242)


# Other

## Symbols
```scala
<-    // Keyword
->    // Method provided by implicit conversion
<=    // Common method
++=   // Can be a common method or syntactic sugar involving ++ method
::    // Common method or object
_+_   // Not really a single operator; it's parsed as _ + _
```

## Keywords/ reserved symbols
```scala
// Keywords
<-  // Used on for-comprehensions, to separate pattern from generator
=>  // Used for function types, function literals and import renaming

// Reserved
( )        // Delimit expressions and parameters
[ ]        // Delimit type parameters
{ }        // Delimit blocks
.          // Method call and path separator
// /* */   // Comments
#          // Used in type notations
:          // Type ascription or context bounds
<: >:      // Upper and lower bounds
<%         // View bounds (deprecated)
" """      // Strings
'          // Indicate symbols and characters
@          // Annotations and variable binding on pattern matching
`          // Denote constant or enable arbitrary identifiers
,          // Parameter separator
;          // Statement separator
_*         // vararg expansion
_          // Many different meanings
```

## Underscore
```scala
import scala._    // Wild card -- all of Scala is imported
import scala.{ Predef => _, _ } // Exclusion, everything except Predef
def f[M[_]]       // Higher kinded type parameter
def f(m: M[_])    // Existential type
_ + _             // Anonymous function placeholder parameter
m _               // Eta expansion of method into method value
m(_)              // Partial function application
_ => 5            // Discarded parameter
case _ =>         // Wild card pattern -- matches anything
f(xs: _*)         // Sequence xs is passed as multiple parameters to f(ys: T*)
case Seq(xs @ _*) // Identifier xs is bound to the whole matched sequence
```

## Syntactic sugars/composition

```scala
class Example(arr: Array[Int] = Array.fill(5)(0)) {
  def apply(n: Int) = arr(n)
  def update(n: Int, v: Int) = arr(n) = v
  def a = arr(0); def a_=(v: Int) = arr(0) = v
  def b = arr(1); def b_=(v: Int) = arr(1) = v
  def c = arr(2); def c_=(v: Int) = arr(2) = v
  def d = arr(3); def d_=(v: Int) = arr(3) = v
  def e = arr(4); def e_=(v: Int) = arr(4) = v
  def +(v: Int) = new Example(arr map (_ + v))
  def unapply(n: Int) = if (arr.indices contains n) Some(arr(n)) else None
}
val ex = new Example
println(ex(0))  // means ex.apply(0)
ex(0) = 2       // means ex.update(0, 2)
ex.b = 3        // means ex.b_=(3)
val ex(c) = 2   // calls ex.unapply(2) and assigns result to c, if it's Some; throws MatchError if it's None
ex += 1         // means ex = ex + 1; if Example had a += method, it would be used instead
```