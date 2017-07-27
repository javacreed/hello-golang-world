# Hello Go Programming Language World

The Go Programming Language is a relatively new programming language developed to address shortcomings that other, more established, programming languages may have.  The Go Programming Language has many benefits, when compared to others, some of which are listed below:

1. **Statically Typed**: One executable file is created which will contain all the code that the program will ever need in order to run on the client machines
1. **Simplified Multithreading Support**: Simply put the `go` keyword before a function call, and you get yourself a thread (you will not get exactly a thread but a *goroutine*, which is a lightweight thread of execution)
1. **Low Memory Footprint**: The Go Programming Language has a smaller memory footprint making it ideal for cases where we may be charged based on the resources our program uses, such as cloud
1. **Fast**: Despite the fact of being a managed programming language, Go is very fast

These are some of the few benefits that the Go Programming Language provides and while this sounds very attractive, Go is very new and lacks the tooling support and the popularity that other main stream languages enjoy.  The lack of tooling support and popularity may prove challenging for someone new to the language and may turn them away.

In this article, we will see how to create a very simple Go program which will print a simple message to the command prompt.  We will build the program and will create an executable file which can be delivered to clients.  While this may sound trivial, some individuals did turn down the language as did not know from where to start.  The motivation behind this article is not to deliver expert advice or to make the reader a Guru, but to help someone new to the language to get quickly started without giving up.  

Some things will be simply mentioned and not much information will be provided in order to avoid overwhelming the reader.  A programming language can easily overwhelm a beginner, who may shy away and we would like to avoid that.

## Install Go

In order for us to be able to develop programs with the Go Programming Language, we need to install the *Go Development Kit*.  This is not usually referred to as *Go Development Kit* (nor *GDK*) but simply *Go* (or *Go Lang*).  Please note that while the developer needs to have Go installed, the client does not require Go to be installed on their machines as Go will produce an executable file which the client can simply execute.

You can download and install Go from the following link: https://golang.org/doc/install.  This page also includes all the information required to install Go.

Once Go is installed, open a command prompt and run the following command.

```
go version
```

This should work and should print the current Go version.  I have installed Go version 1.8.3 and I am running this on Windows 64 bit machine and following is the output of my Go version.

```
go version go1.8.3 windows/amd64
```

Kindly note that you may get a different output depending on your version of Go and on the operating system you are using.  While the version or the operating system will not affect this article, some artefacts are operating system specific.  For example, windows make use of executable files with the `.exe` as their extensions.  Other operating systems do not use this approach and do not have file extensions.

Should you encounter any difficulties installing Go, please do not hesitate to contact me at *albert@javacreed.com*

## Create Project

With Go installed, we can go ahead and create our first program.  In order to keep with the tradition, our first program will be nothing but a simple hello world program.  Unfortunately, we need to do several things before we can start coding.  The following sections will describe what needs doing before we can start programming with Go.

### Workspace and the `GOPATH` Environment variable

Go programs are organised within a workspace.  A workspace can host one or many programs.  Within a workspace, we will find all the code that the program will ever use, which includes all third party dependencies.  For example, if a program uses an existing library, both this program and the existing libraries are found under this one workspace.  While this is not necessarily required (to just have one workspace for all Go programs), it is simpler to have one workspace and put all your projects under this workspace.  You will find fewer obstacles if you use one workspace for all your code.  Note that this does not mean that you will have everything in one folder.  On the contrary.  As we will see later on, we will still organise the code in different folders and we will not have a mess.

This may be a bit confusing at first and may take some time to get your head around it.  Given that we will start with a simple hello world program, we do not need to worry too much about it.  Furthermore, this article will walk us through each step to make sure that everyone reading this article is able to create a working program, irrespective of his/her experience.  All you need to appreciate is that with Go, all code, including the dependencies, are saved under one workspace.

Let us create a directory called `golang` and use this as our workspace.  This directory can be created *almost* anywhere and you can have *almost* any name you like.  I have created this directory in the following path `C:\Users\albert\Work\golang`, but as mentioned before, this can be created *almost* anywhere you like.  I have used the word *almost* here as you cannot create the workspace in the same path where Go was installed.  Also, try to keep the paths short to avoid hitting OS path length limits.  Other than that, you are free to be creative.

Once we decide what to call our workspace directory and where to create it, we need to configure the `GOPATH` environment variable to point to the workspace directory.  This environment variable is used by various parts of the Go Programming Language and needs to point to your workspace.

Different operating systems have different approaches to how to manage environment variables.  In Windows, you can configure the `GOPATH` from the command prompt as shown below, or through the Environment Variables window.

```
SET GOPATH=C:\Users\albert\Work\golang
```

Confirm that the `GOPATH` environment variable is properly created by printing its value as shown next.

```
ECHO %GOPATH%
```

This should print the path of our workspace.

Recall the "*one workspace recommendation*" mentioned before.  With multiple workspaces, we would need to change the `GOPATH` environment variable every time we switch workspaces.

### Workspace Structure

We want to create a simple program, and yet we are already overwhelmed with things that we need to do.  We can use tools, such Maven (https://maven.apache.org/) and `mvn-golang` plugin (https://github.com/raydac/mvn-golang) to assist us, but I believe that is a steeper path for someone new, so decided to go manual.  Please note that I like Maven and I use Maven a lot.  Most of the programs I work with use Maven and in no way, I am discouraging anyone from using Maven.  On the contrary.  I believe that Maven is a great tool and one should definitely use it.  I just do not think that here (being a simple program) is the right place.

A Go workspace consists of three folders, named:
1. `src`
1. `pkg`
1. `bin`

Without diving too deep, the `src` folder will contain all source code, including any dependencies we import.  These are organised into sperate sub-directories to keeps things well organised and separate.  Any executables we build are saved under the `bin` folder while the `pkg` folder will contain packaged objects.  We do not need to worry about the last two folders as we will be working mainly with the `src` folder for now and these were mentioned here for completeness.

Programs (mainly their source code) are usually saved within repositories such as Git (https://git-scm.com/) and the famous GitHub (https://github.com/).  The source code for this example is committed to https://github.com/javacreed/hello-golang-world from where anyone can check it out (using `git clone https://github.com/javacreed/hello-golang-world` or other means).  You do not need to checkout this code, as we will be building everything from scratch.

**Why is this relevant to the Go Programming Language?**

The `src` folder is organised around the source repositories such as Git and GitHub.  Given that my example is saved in GitHub, I have created the following structure

```
golang/                        # My workspace
  bin/                         # Empty for now
  pkg/                         # Empty for now
  src/                         # Where all source code is saved
    github.com/                # All source/projects whose repository is
                               #   GitHub are found under this subdirectory
      javacreed/               # My GitHub username
        hello-golang-world/    # The project name
          .git                 # Git repository metadata for this project
```

The above structure shows how the project and its source code are typically organised under the `src` folder.  You can use a different layout, but that is not recommended as Go follows this layout.  For example, when importing other projects from GitHub, the imported projects are saved in a structure like the one shown above.

One needs to understand the relation between workspace and project.  The project is a part of a workspace and a workspace may have one or more projects.  The workspace itself does not go into a repository such as Git and GitHub.  On the other hand, each project can have its own repository.  For example, we can check out two different projects from GitHub into the same workspace.  Following the layout showed here, these two projects will never conflict, as they will be saved in different directories.  Each project will have its own repository.

**What should one do if they do not have a GitHub account or do not want to save this code in GitHub?**

There are two ways about it:

1. Create a GitHub account from: https://github.com/join?source=header-home (it is free).  I believe that all developers should have an account
1. Create another folder instead of `github.com` and call it `local` as shown next.

```
golang/                        # My workspace
  bin/                         # Empty for now
  pkg/                         # Empty for now
  src/                         # Where all source code is saved
    local/                     # All source/projects without repository are
                               #   found under this subdirectory
    hello-golang-world/        # The project name
```

Under the `local` folder you can have as many projects as needed, all under one workspace.

## Writing Our First Go Program

Finally, we got to the part where we actually write some Go code.  This is quite challenging for someone new to the language and to programming in general as too much is expected from him/her, even before they start.

Go programs are simple text files with the `.go` file extension.  Create a file called `hello.go` under the `hello-golang-world` (`src\github.com\javacreed\hello-golang-world`) folder.  Open this file using any text editor you like.  It does not matter which text editor you will use for now.  All we need is a simple text editor where we can copy the following example and get started.

``` go
package main

import "fmt"

func main() {
    fmt.Println("Hello Go Lang World!!")
}
```

I hate it when I am told to do something without understanding why I am doing it, and here I am asking you to do just that.  Do not worry about this for now as we will cover each part later on.

Our `hello.go` file now contains the code shown above and we are now ready to take this code for a spin.

## Run Our First Go Program

From here onwards, it is all downhill.  Running a Go program is fairly simple as shown next.  Navigate to where your `hello.go` file is and invoke the `go` command with the `run` as the first command line argument as shown next.

```
go run hello.go
```

This will run your Go program and will output the following

```
Hello Go Lang World!!
```

As promised before, this cannot be any simpler.  We ran our first Go program.

## Package Our First Go Program

Now that we are all excited about our first Go program, we would like to send it to all our friends so they can see our creation.  This can be easily achieved by simply using the `install` command line arguments as shown next.

There are several options to install a Go program and thus creating the executable version.  The first option is to install it from the workspace (the path where the environment variable `GOPATH` points) as shown next.

```
go install github.com\javacreed\hello-golang-world
```

Note that here we did not include the `src` in the path.  That is because the `install` command line argument takes the model name.  Alternatively, we can navigate to the package itself (`src\github.com\javacreed\hello-golang-world`) and execute the following instead.

```
go install .
```

All these will yield the same result and produce the `hello-golang-world.exe` executable file which is saved under the `bin` directory.  Note that different operating systems mat produce a different artefact.  Whenever we install a program, the generated artefacts are saved under the `bin` or `pkg` directories.

Navigate to your `bin` directory and you should see your new executable file.  You can run this file from the command prompt and you should see the same output as before.

```
Hello Go Lang World!!
```

This file contains all our code and running it will run our program.  Here we created a trivial application, but this is a very powerful concept as you do not need to worry about external libraries (such as JARs or DLLs) as all is contained in one file.  Furthermore, Go created a file that is ready to run and thus you do not need to any install platforms or frameworks (such asn Java or JEE servers) for your program to run.

With Go we can easily create executable files for a different operating systems (known as *cross compiling*) by setting the correct environment variables as described in the article found at: https://github.com/golang/go/wiki/WindowsCrossCompiling.  For those familiar with cloud computing, this is ideal as all you need to do it deploy your single file anywhere you need to and just run it.

Alternatively, we could have used the `build` as the first command line argument instead of the `install`, which only builds the executable files without installing them.  By "*installing them*" I mean saving the created artefacts under the `bin` (or `pkg` - see side note at the end of this paragraph) folder.  I did some research about the differences between these two options and was not able to find a valid reason why one option should be picked over the other and given that `install` seems to be the superset, I felt that it was the right way to go.  With that said, I am confident that the `build` command line argument has its place, but unfortunately, it is still a mystery to me.  A side note, not everything goes to the `bin` folder. Libraries or utilities are compiled once and saved under the `pkg` folder instead to be reused when needed.

## Go Syntax

As promised before, in this section we will go through the syntax used in this example.  In order to keep things simple, only the syntax used in this example is described.

Following is the program we played with during this article.  We had to go through a long walk before being able to write and run these 5 lines of code.  This is quite inefficient and hopefully, one-day, programming becomes more accessible.

``` go
package main

import "fmt"

func main() {
    fmt.Println("Hello Go Lang World!!")
}
```

The program will be divided into several smaller parts and each part of this program is analysed and described in some depth.  We will only limit ourselves to the code we have here but will try our best to cover this as comprehensively as possible.

### Package

Go programs belong to packages and this is defined as the first line of our example.

``` go
package main
```

Here we defined that our program belongs to the `main` package.  A Go file can only have one package and the package is independent of the file system and the folder where the file is found.  In other words the, we are free to pick any package name we like as long at it is valid.  Please refer to this page: https://golang.org/doc/effective_go.html#package-names for a comprehensive description of valid package names.

**So if we can pick any name we like, why `main`?  Was this randomly pick?**

The best way to answer that is to try it out.  Let us change the package name and try to run our program again.  The package is changed to `hello` instead of `main` as shown next.

``` go
package hello

import "fmt"

func main() {
    fmt.Println("Hello Go Lang World!!")
}
```

Navigate to where your `hello.go` file is and invoke the `go` command with the `run` as command line argument as shown next.

```
go run hello.go
```

Running the program will produce the following error:

```
go run: cannot run non-main package
```

As the error implies, we are trying to run a program which package is not `main`.

**So if the package needs to be `main` why should we define it in the first place?**

Our example consists of one file.  Larger projects will have many files and these can be organised in different packages.  The most important thing is that our starting point is in the `main` package.  In other words, a program can have many files, but it needs to have one file with the `main` package.  This will be the starting poit of the program.

Packages serve different purposes.  These help us organise our code and also allows us to restrict access to certain parts of our code. I found a house to be a good analogy for packages.  In a house, we have many rooms such as the kitchen, bathroom, bedroom and the like.  Things within the house are organised in their respective rooms.  For example, towels are found in the bathroom, while bed sheets are found in bedrooms.  Same applies to code.  The mathematically related code is found in the `math` package while input/output related code is found in the `io` package for example.

Rooms in the house can be locked from the inside and thus one cannot go inside the locked rooms (assuming that you cannot open these with a key).  Same applies to packages in the code.  We can limit access to certain parts of the code only to other code from within the same package.  In other words, *part a* of the code can only access *part b* if and only if *part a* is within the same package as *part b*.  Unfortunately, in order to provide a more concrete example, we need to touch other aspects of the syntax which we have not yet covered and make things more complex.

### Import

Programs reuse existing code in order to avoid code duplication and to simply focus on the task at hand.  We do not build a TV, but we simply use a TV built by someone else, for example. Our program prints a message to the command line, yet we did not write any code that actually outputs text to the command prompt.  Instead, we used existing code, which took our text and printed it on the command prompt.

The `import` statement is used to include other existing packages into our program and make use of code shared by the imported packages.  Here we imported the package named `fmt` which contains formatted I/O functionality.  More information about this package and its content can be found at: https://golang.org/pkg/fmt/.

``` go
import "fmt"
```

Any code we use from imported packages needs to be prefixed with the package name as shown next.  

``` go
    fmt.Println("Hello Go Lang World!!")
```

The `PrintLn()` code had to be prefixed with the package name `fmt` because this belongs to the `fmt` package.  Some packages may have long names and the `import` statement allows us to provide an alias instead as shown next.

```
import f "fmt"
```

The imported package `fmt` is given an alias of `f`.  Now we can simply use the alias instead of the package name.

```
    f.Println("Hello Go Lang World!!")
```

We have not yet covered the `PrintLn()` and it is normal to be a bit confused.  Unfortunately, at the beginning, you are exposed to too many different things that are all interconnected and yet we need to learn these interconnected things one by one.  The `PrintLn()` is a function found in the `fmt` package.  But feat not as functions are described next.

### Functions

Another keyword that the Go Programming Language has is the `func` keyword which represents a function.  

**What is a function?**

Say you want to find the largest from two numbers.  How will you do this in real life (not with a program)? You will compare the two numbers in your head and will return the largest one.  Programs use functions to solve such problems and handle such cases.  The function will take a set of numbers, will find the largest one and returns it.  Functions can do other things as well, such as printing a message to the command prompt like our example and much more.

``` go
package main

import f "fmt"

func main() {
    f.Println("Hello Go Lang World!!")
}
```

We have one function called `main`

``` go
func main() {
}
```

The function name can be any valid name but as you may have guessed `main` has an important meaning and was not randomly picked.  And that is correct.  A file can contain many functions as long as each function has a unique name.  You cannot have two or more functions with the same name in the same file (or in different file but in the same package).  Remember that different files can have the same package.  To make this clear, you cannot have two files in the same package with a finction of the same name in each file.  Furthermore, Go does not support function overloading (https://en.wikipedia.org/wiki/Function_overloading) like other languages do.  

**If a file can have many functions, from where will the program start?**

The program will always start executing from the `main()` function.  The `main()` function is the starting point of a program.  A Go program can have many files and each file can have many functions, but it needs to have one file with the `main` package and the `main()` function.

Functions can take arguments and can return values and errors as well.  Our program made use of a function written by someone else.  This is the `Println()` function, which takes a number of arguments and then displays these arguments to the command prompt.

Being a primitive example, we did not use return values and error handling.  Go functions can return nothing, one or more results and can also return errors.  We will not cover the errors here as otherwise, we will never finish.  But bear in mind that different from many other programming languages, in Go, a function can return more than one value.  For example, the function `sumAvg()`, shown below, takes two numbers and returns both their sum and their average.

``` go
func sumAvg(m, n int) (sum, avg int) {
    sum = m + n
    avg = sum / 2
    return
}
```

In the above example, we also made use of the *named return values* (https://tour.golang.org/basics/7) which is another feature that the Go Programming Language supports.

## Conclusion

In this article, we saw how to create a simple hello world program with the Go Programming Language.  I believe that after given a few pointers, one can easily get going with Go.  The Go programming language is very concise which makes it easier to learn.  The language is very opinionated and thus you need to have things "*the Go way*".  Past that, the rest should be straight forward.  I hope that this article can help anyone with any experience level to get going with Go.
