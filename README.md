### learning-groovy - http://docs.groovy-lang.org/latest/html/documentation/

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
###### Operator Overloading (+, - , *, [] internally called getAt method of string, == internally called equals method)
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
* Multiline String
```
def textAreaString = '''Hi This is multiline string
hahahahah'''
```

```
def textAreaString = """Hi This is multiline string
hahahahah ${1 + 1}"""
```
* Slashy String (used for regex expression, see https://docs.oracle.com/javase/tutorial/essential/regex/pre_char_classes.html)
```
def fooPatern = /.*foo.*/
assert fooPattern == '.*foo.*'

def testString = 'Hello , regex !'.toLowerCase.replaceAll(/\W/,'')  ``` \W looks for non [a-zA-Z0-0_] ```
assert testString == 'helloregex'
```
 * Using tilde on a slashy string converts it inotRegex Pattern
 * assert ~/abcd/ instanceof java.util.regex.Pattern
##### POGO (POJO in Java, POPO in Python)
```
class Person {
 String first
 String last
}


Person p = new Person()
p.setFirst('Neeraj')
p.last = 'Mahajan'
println "${p.getFirst()} ${p.last}"
```
###### Key points
* By default class is public.
* By default methods are public.
* By default attribute(instance variables) are private.
* If we don't specify private or public on attributes, Groovy by default generates setter and getters.
* If we want groovy not to provide setters, then make it final.
* When we assign object.attribute(p.last = 'Mahajan') then it internally called setter method.
* When we access object.attribute(p.last) then it internally called getter method.
* In Groovy, we can call the constructor with map of key:value **(Json object)** then it will internally create a class and initialize the instance variables. eg ``` Person p = new Person(first:'Neeraj',last:'Mahajan') ```
* In groovy method, last evaluate expression is retured. We don't need an explicit **return** keyword.
* **import groovy.transform**
  * @ToString : automatically provide toString method implementation. default format ``` className(comma separated instance variable values).
  * @ToString(includeName=true) : chages the default format to ``` className(comma separated key:value )```.
  * @EqualsAndHashCode : provide equals and hasCode method implementation based on all instance variables comparison.
  * @TupleConstructor : generate constructors (constructor values will be injected in the order of declaration on instance variables).
  * @Canonical : Wrapper for all above annotations.

##### Collections
###### Range
```
Range r = 1..10
println "$r"           // [1,2,3,4,5,6,7,8,9,10]
println r.from         // 1
println r.to           // 2
println r.contains(5)  // true
r = 1..<10
println "$r"           [1,2,3,4,5,6,7,8,9]
```
###### List
```
List nums = [7,1,2,7,77]
println nums                                         // [7, 1, 2, 7, 77]
println nums.class.name                              // java.util.ArrayList
println nums[1..3]                                   // [1, 2, 7]
println nums - 7 - 1                                 // [2, 77]        
println nums * 2                                     // [7, 1, 2, 7, 77, 7, 1, 2, 7, 77]
println nums + [11,12]  !! Create a new list         // [7, 1, 2, 7, 77, 11, 12]        
println nums                                         // [7, 1, 2, 7, 77]
nums << [13,14]         !! Appends to list                               
println nums                                         // [7, 1, 2, 7, 77, [13, 14]]
[1,2,[3,4,5],[6,7],[8,9,10,11,[12,13],14]].flatten() //  [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]                                

```

###### Set
```
def map = ['a':1,b:2,c:3]              // 
println map                            //[a:1,b:2,c:3]
map.put('d',4);                        //
map['e'] =5;                           //
map.f = 6;                             //
println map                            //[a:1,b:2,c:3,d:4,e:5,f:6]
println map.getClass().getName()       // java.util.LinkedHashMap
```
