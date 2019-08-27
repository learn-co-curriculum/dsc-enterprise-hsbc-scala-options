
# Option

## About Option

* If I ask you if you have a middle name you’d either answer:
  * Yes
  * No
* If it is yes, I might press further and ask "What is it?"
* That is how `Option[T]` works
* It is also a way that we avoid `null`
* `null` is still available to interoperate with Java and its libraries

## The problem with null

Apologies from Tony Hoare 2009

_"I call it my billion-dollar mistake. It was the invention of the null reference in 1965. At that time, I was designing the first comprehensive type system for references in an object oriented language (ALGOL W). My goal was to ensure that all use of references should be absolutely safe, with checking performed automatically by the compiler. But I couldn’t resist the temptation to put in a null reference, simply because it was so easy to implement. This has led to innumerable errors, vulnerabilities, and system crashes, which have probably caused a billion dollars of pain and damage in the last forty years."_

## The ambiguities of null

If in a database, the middle name field has a `null`, does it mean:

* The person doesn’t have a middle name
* No one has entered the middle name

## `Option[A]`

* `Option[+A]` is the super type of `Some[T]` and `None`
* `Option[+A]` is an `abstract class`

https://www.scala-lang.org/api/current/scala/Option.html

## How it is used:

Using `Some`


```scala
val middleName = Some("Antony") //type is inferred as Some
val middleName2:Option[String] = middleName
val middleName3:Some[String] = middleName
```




    middleName: Some[String] = Some(Antony)
    middleName2: Option[String] = Some(Antony)
    middleName3: Some[String] = Some(Antony)
    



Using `None`


```scala
val noMiddleName = None //Singleton
val noMiddleName2:Option[Nothing] = noMiddleName
val noMiddleName3:None.type = noMiddleName
```




    noMiddleName: None.type = None
    noMiddleName2: Option[Nothing] = None
    noMiddleName3: None.type = None
    



## How do we interact with an `Option`?

To interact with an Option we can either call:

* `get` (Dangerous)
* `getOrElse` (Safe)
* Pattern Matching (Whoa)
* Functions (Sweet!)


```scala
middleName.getOrElse("N/A") //Antony
noMiddleName.getOrElse("N/A") //N/A
```




    res1: String = N/A
    



If we chose `get` we run the danger of the last one of throwing an exception


```scala
middleName.get //Antony
noMiddleName.get // java.util.NoSuchElementException: None.get
```


    java.util.NoSuchElementException: None.get

      at scala.None$.get(Option.scala:347)

      ... 37 elided

    


## Getting the info using Pattern Matching:
If we had a method that received an `Option[T]` we can use pattern matching to break it apart and analyze it


```scala
def whatIsTheMiddleName_?(x:Option[String]):String = {
   x match {
     case Some(a) => a
     case None    => "N/A"
   }
}
whatIsTheMiddleName_?(Some("Carmen"))
```




    whatIsTheMiddleName_$qmark: (x: Option[String])String
    res5: String = Carmen
    



Here we can break up the `Option[T]` by specifically asking what particular type we are looking at, a `Some` or `None`

If it is a `Some`, extract the value and return, if it is a `None` return "N/A"

## `Option` Conclusion

* Scala programmers despise `null`, so we use `Option`
* Options are modeled as `Some` or `None`, and if `Some`, we can extract the answer.
* Extracting the answer can be done by calling `get`, `getOrElse`, or pattern matching, or functions (though we haven’t discussed functions yet)
* Scala still has `null` to interoperate with Java, but in a pure Scala application, don’t use `null`.
