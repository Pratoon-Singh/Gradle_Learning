
# Gradle Learning with [Gradle Link] (https://www.youtube.com/watch?v=R6Z-Sxb837I&t=2098s)

To Intialize the gradle project :- gradle init in the respective folder.
To Compile java classes :- ./gradlew compileJava
To add resources to the build folder ./gradlew processResource
To build a jar of the java project :- ./gradlew jar
To run the jar of the java project :- java -jar "path for the jar.jarname.jar"
for Eg :- java -jar build/libs/java.jar
To Run Tests:- ./gradlew test

3 diffrences in kotlin and java

Kotlin is a scripting language running in jvm
1.) Semicolons are optional in Kotlin
    val name = "Bob"
    println(name)
        Output:- Bob

2.) String supports interpolation by default
    var name = "Bob"
    println("His name is ${name}"
        Output :- His name is Bob

3.) val is for read only variables and var for mutable variable
    var mutableName = "Bob V2"
    mutableName = "Bob v1"
    prinln("New and improved name ${mutableName}")
        Output:- New and improved name Bob v1

Feature 2 lambda expression :-

lambda expression = pass function around and execute later

val lambdaExp={
for(i in 3 downTo 1){
println(i)
}
println("lift off")
}
When called lambdaExp()
Output:- 321 lift off

Used heavily in gradle build scripts

repositories{
mavenCentral()
}
paranthesis normally required to call function
       dependencies{
           testImplementation("org.junit.jupiter:junit-jupiter:5.10.0")
       }

when lambda expression is final argument , paranthesis are optional
      repositories{
      mavenCentral()
      }

1.)allows fast lookup of what code you can run in a Gradle build
2.)helps you understand more advanced gradle features later on

# The Task Graph
task can depend on other tasks
Build depends on assemble and check
Build doesn't do anything itself
build aggregates and check tasks
Assemble handles building your project including artifacts such as jar files and check Handles testing your projects


# Java plugin task graph
    :build  *
        $:assemble  *                                             @ = task which performs an action
            @:jar   *                                             $ = aggregate tasks (does'nt performs any task when it runs for eg:- classes aggregates compileJava and processResources)
                $:classes                                         * = important task to remember
                    @:compileJava                                 o can choose specific task to save time
                    @:processResources                                  o check(just need to test the project)
        $:check  *                                                      o assemble(just need to build the project)
            @:test  *
                $:classes
                    @:compileJava
                    @:processResources
                $:testClasses
                    @:compileTestJava
                        $:classes
                            @:compileJava
                            @:processResources
                    @:processTestResources


To clean the build folder :- ./gradlew clean
To build the project with jar :- ./gradlew assemble
To test the project without assembling everyting in your project :- ./gradlew check
