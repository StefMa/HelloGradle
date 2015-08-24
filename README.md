# Download and Install gradle
## Donwload
Go to http://gradle.org/gradle-download/ and download the latest gradle version. Unzip the file and put the extracted folder anywhere you like.
## Install
Well here is nothing to do :)
You can put the `bin/` folder to your path. For this open the `~/.bash_profile` and put the following line in this:

    # The next line updates PATH for gradle-2.6
    export PATH="/Path/To/Your/Extraced/Gradle/Folder/gradle-2.6/bin:$PATH"

Now you can run in your terminal

    gradle
and get a output like this:

    :help

    Welcome to Gradle 2.6.

    To run a build, run gradle <task> ...

    To see a list of available tasks, run gradle tasks

    To see a list of command-line options, run gradle --help

    To see more detail about a task, run gradle help --task <task>

    BUILD SUCCESSFUL

    Total time: 1.302 secs

# Gradle Wrapper (git hash: ccd2c06)
## What is it
A gradle wrapper can be used for shipping gradle to other developers which don't needed to install gradle by thereself. The wrapper automaticly download and "install" gradle on the developer machine so that the other developers can run gradle like it is installed.
## Setup
To enable the wrapper just run

    gradle wrapper
That's all. Gradle will automatically make a `gradle/wrapper/` folder and two files. The `gradlew` bash script and the `gradlew.bat` script (last is for windows users).
To run the wrapper (and without explicied installation of gradle) just call

    ./gradlew
and you will see the same help message like above (under installation).

# Setup tasks (git hash: 55d73ce)
## build.gradle File
First of all you need a `build.gradle` file. Got to your project directory and make the file.
Put these code in it:

    task hello << {
        println 'Hello world!'
    }
## Run the task
Now you can run these tasks with

	gradle hello
to use the "machine" gradle installation.
Or run the tasks with the wrapper

	./gradlew hello

# Java plugin (git hash: 34a2044)
## What is it
The gradle Java plugin brings your project support for Java compilation along with testing and bundling capabilities.

## Setup
To make your project to a "`gradle java`" project you only need one line of code. Put on the head of your `build.gradle` the following line

	apply plugin: 'java'
For later useage we need also the `application` plugin to run our java code. So put also:

	apply plugin: 'application'

Your file looks now like this

	apply plugin: 'java'
	apply plugin: 'application'

	task hello << {
	    println 'Hello world!'
	}

# Time to code (git hash: 5104f28)
## Java main method
For testing our gradle setup we need some java code. Put a new class named TestGradleSetup to your `src/` folder and put the `main` method in it

	public class TestGradleSetup {

	    public static void main(String[] args) {
	        System.out.println("Yes, it works!");
	    }
	}

## Our build.gradle
We need to tell gradle where the main method is located. For this we must open our `build.gradle` again and configure the main class

	mainClassName = "TestGradleSetup"
The variable `mainClassName` cames from the `application` plugin. So gradle nows what they can do with that.
We also need to chance the `sourceSet` from our java plugin. Because the default value is 

    [${project.projectDir}/src/${sourceSet.name}/java]

But our class is directly in 

    [${project.projectDir}/src/}
So put these also in your `build.gradle``

	sourceSets.main.java.srcDirs = ['src']
Our full gradle looks now like this

	apply plugin: 'java'
	apply plugin: 'application'

	task hello << {
	    println 'Hello world!'
	}

	sourceSets.main.java.srcDirs = ['src']
	mainClassName = "TestGradleSetup"

## Run and stay happy
Now we can finally run 

	./gradlew run -q
and get our hoped result

	Yes, it works!
