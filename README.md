# Setting up Scala environment for local development

In this post, we’d go though the process of setting up a local Scala development environment and run a “Hello World” program. This is first in a series of posts which will culminate in creating a template for Serverless Data Lake using [Apache Spark](https://spark.apache.org "Apache Spark").  

“_Scala combines object-oriented and functional programming in one concise, high-level language. Scala's static types help avoid bugs in complex applications, and its JVM and JavaScript runtimes let you build high-performance systems with easy access to huge ecosystems of libraries._” - Official [Scala](https://www.scala-lang.org) website.

## Setting up the code editor
Before we start writing code, we’d need to setup either an IDE like _Eclipse or Intellij Idea_ or a code editor like _VS Code_.  

For this post, we’d go ahead and setup VS Code from Microsoft which is a free and light-weight code editor along with some extensions exclusively for Scala Development

* VS Code is [available for free](https://code.visualstudio.com) from Microsoft Website with pretty detailed set-up [instructions](https://code.visualstudio.com/docs/setup/setup-overview).
* Next, we’d need two plugins to aid us in Scala development which are the [Scala Syntax](https://marketplace.visualstudio.com/items?itemName=scala-lang.scala) plugin and the [Sbt](https://marketplace.visualstudio.com/items?itemName=lightbend.vscode-sbt-scala) plugin from Lightbend.
![](images/Screen%20Shot%202020-05-24%20at%208.50.07%20PM.png)
## Installing sbt
Next, we’d need to install sbt _aka_ Scala Build Tool, which is a build tool for Scala, Java and more. Detailed instructions on installing sbt are available [here](https://www.scala-sbt.org/1.x/docs/Setup.html).

If you are using a Mac with [Homebrew](https://brew.sh) installed like me, you can install it using `brew install sbt`.

## Creating a new Project
Once we have sbt installed, we can go ahead and initialize a new Scala project by running the `sbt new sbt/scala-seed.g8` command on the command line.
![](images/Screen%20Shot%202020-05-24%20at%208.38.16%20PM.png)

Once we have initialized the project, we can open it up in the VS Code editor by running `code .`
![](images/Screen%20Shot%202020-05-24%20at%208.40.29%20PM.png)

## Writing code
By seeding the project while initializing using sbt’s provided template, a “Hello World” is created by default.

```scala
package example

object Hello extends Greeting with App {
  println(greeting)
}

trait Greeting {
  lazy val greeting: String = "hello"
}

```

A file containing tests is also generated

```scala
package example

import org.scalatest._

class HelloSpec extends FlatSpec with Matchers {
  "The Hello object" should "say hello" in {
    Hello.greeting shouldEqual "hello"
  }
}

```

And, finally the _build.sbt_ file where we can define dependencies is also generated

```scala
import Dependencies._

ThisBuild / scalaVersion     := "2.12.8"
ThisBuild / version          := "0.1.0-SNAPSHOT"
ThisBuild / organization     := "com.example"
ThisBuild / organizationName := "example"

lazy val root = (project in file("."))
  .settings(
    name := "Hello Scala",
    libraryDependencies += scalaTest % Test
  )
```

## Building and Running
To run our simple app, we will use the sbt shell. 

* Open a terminal and navigate to the project directory containing the _build.sbt_ file  
	`cd hello-scala`
* Type `sbt` and hitting run. This would initialize the sbt shell.  
	![](images/Screen%20Shot%202020-05-24%20at%209.05.31%20PM.png)
* To run the program, just type `run` and hit enter.  
	![](images/Screen%20Shot%202020-05-24%20at%209.08.09%20PM.png)
* To exit the sbt-shell, type `exit`

In this brief post, we learned about setting up a Scala “Hello World” project on using sbt. Please let me know if you faced any issues following this or if parts are unclear.
