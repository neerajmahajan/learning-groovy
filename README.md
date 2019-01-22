# learning-groovy

#### Intro

* Most Matured JVM based dynamic language(optionally typed datatype) and easiest for java developers to learn.
* can mixed java and scala in same codebase.
* Other Major dynamic languages
  * Scala - statically typed, suitable for concurrrency , functional.
  * Clojure - specifically for functional programming.
  * Hybrid languages - compile to bytecode
    * JRuby
    * Jython
##### Installation (java should be pre-installed)
* Zip file
* Installer
* Groovy environment manager (gvm) - support installing multiple version of technology stack (groovy, grail,gradle,griffin etc)

##### Running groovy
* groovyc
* groovy
* groovy shell
* Executing groovy without compiling it
* groovy -e "println InetAddress.localHost"

###### Programming structure

* Everything is object oriented
* semicolon are optional.
* can mix java code.
* println("Hello World");
* paranthesis are optional eg ``` println "Hello World" ``` will work and ``` println 'Hello World' ``` will also work. note single quotes
* String can be put in single quotes or double quotes
  * "" can be used for evaluating strings expression, where as '' are normal java type strings.
  * ```
      void sayHello(String name) {     
      println "Hello, ${name}"
      println('Hello World');
    }
    ```
##### Groovy script
* Create a file with any name with .groovy extension 
* compile and execute eg groovy hello_world.groovy then groovy hello_world
* directly execute eg groovy hello_world.groovy
* run compiled code with java eg java hello_world (use javap to see how java class is created from groovy script)
 * any variable created in script become local variable in main method
 * before executing groovy script from java add groovy to classpath
   * java -cp $GROOVY_HOME/embeddable/groovy-all-2.4.3.jar:. hello_world ?? find how it works in 2.5.5
##### Asserts, imports and def

* Assert 
```
int x = 3
int y = 4
assert 7 == x + y +1
```

* Import
 * Groovy has lot of automatic imports which includes
   * java.lang.*
   * java.util.*
   * java.net.*
   * java.io.*
   * java.math.BigInteger
   * java.math.BigDecimal
   * groovy.lang.*
   * groovy.util.*

* def Keyword (dynamic typing similar to var in javascript)
 * We use def when we don't want to specify datatype or datatype is not known.
 * eg def x =1
      println x.getClass().getName()
 * If we have declared the variable with def, then we can change the value of different data types.
 
 ##### Data Types 
 * Everything is an Object in groovy
 * eg 3.getClass().getName() will return java.lang.Integer ,(3.5).getClass().getName() will return java.math.BigDecimal
 * By default groovy uses high precision data types eg 3.5 is BigDecimal by default instead of float.
 * When we use operators on numeric type, groovy internally invokes corresponding methods in API.(Operator overloading)
  * 2.0 - 1.1 is same as 2.0.minus(1.1)
 ###### Strings vs Java String
 * def javaString = 'this is a string'
   * javaString.getClass().getName() will return java.lang.String
 * def anotherJavaString = "this is another Java String"
   * anotherJavaString.getClass().getName() will return java.lang.String
 * def groovyString = "this is Groovy string ${1 + 1}"
   * groovyString.getClass().getName() will return org.codehaus.groovy.runtime.GStringImpl
###### Operator Overloading (+, - , *)
* - will remove first occurence of passed string
* * will repeat and concat the string x times.
```
def s = 'this is all'
  s -  'is'  will return  'th is all'
  s * 2 will return 'this is allthis is all'
  s[0] will give t
  s[-1] will give l
  s[-2] will give l
  s[-3] will give a
  s[0..3] will give 'this' from and to are both inclusive
  s[-3..-1] will give 'all'
  s[-1..-3] will give 'lla'
  s[0..3,5..6.8..-1] will give 'thisisall'
```
