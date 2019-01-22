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
