# Simple Makefile Tutorial
How to create a personalized Makefile for simple programs. 

**README IN PROGRESS**

<p align="center">
  <img width="237" height="81" src="readmeimage.jpg">
</p>

If you've ever gone to college for Computer Science, at some point in time your professor will ask for a Makefile. More often than not, they will assume that you know how to make one, or just leave you to your own devices. Let this be your go-to device. 

![](header1.jpg)

## Generic Makefile Template

## Ada Makefile Template
For a single .adb Ada project file:
```sh
TARGET = [Insert Executable Name Here]

$(TARGET):
        gnatmake -f -o $(TARGET) -q main.adb -cargs -bargs -l
#
# Clean the src dirctory
#
clean:
        rm -rf *.o
        rm -f *.tar
        rm -f $(TARGET)
        rm -f *.ali

```
Replace main.adb with the name of your file.

For an Ada project with multiple object files:
```sh
TARGET = [Insert Name of .adb file here]
OBJECTS = main.o kbd.o command.o display.o \
          insert.o search.o files.o utils.o

$(TARGET) : $(OBJECTS)
        gnatmake -o $(TARGET) $(OBJECTS)
main.o : main.c defs.h
        cc -c main.c
kbd.o : kbd.c defs.h command.h
        cc -c kbd.c
command.o : command.c defs.h command.h
        cc -c command.c
display.o : display.c defs.h buffer.h
        cc -c display.c
insert.o : insert.c defs.h buffer.h
        cc -c insert.c
search.o : search.c defs.h buffer.h
        cc -c search.c
files.o : files.c defs.h buffer.h command.h
        cc -c files.c
utils.o : utils.c defs.h
        cc -c utils.c
clean :
        rm edit $(OBJECTS)
```
The -o option specifies the name of the executable file. To have the name of the executable be different from the program name, simply replace the $(TARGET) after -o on line 6 to the name you desire. Please Note that this Makefile does use the GCC compiler along with gnatmake compiler.

## C Makefile Template
The Simple C Makefile:
```sh
  # build an executable named myprog from myprog.c
  all: myprog.c 
 	  gcc -g -Wall -o myprog myprog.c

  clean:
	  $(RM) myprog
```
Use your brain - fill in the blanks to customize. If your program is called main.c, then replace myprog.c with main.c. This makefile template uses the GCC compiler.

Makefile Template for multiple object files:
```sh
#  -g    adds debugging information to the executable file
#  -Wall turns on most, but not all, compiler warnings
#
# for C++ define  CC = g++

CC = gcc
CFLAGS  = -g -Wall
TARGET = [Insert Executable Name Here]
OBJECTS = name.o, [List .o Files Here]

default: $(TARGET)

$(TARGET):  $(OBJECTS) 
	$(CC) $(CFLAGS) -o $(TARGET) $(OBJECTS)

# To create the object file name.o, we need the source
# files name.c, and any neccesary .h files:
#
name.o:  name.c possible.h possibletwo.h 
	$(CC) $(CFLAGS) -c name.c

#Repeat this for all the .o files included in your program

clean: 
	$(RM) count *.o *~
  ```
 Typing 'make' or 'make Insert_Executable_Name_Here' will create the executable file. 'make' will invoke the first target entry in the file (which here is the default entry). To start over from scratch, type 'make clean'. This removes the executable and old .o object files as well as any ~ backup files.
## Python Makefile Template
This great Python makefile from Krzysztof Żuraw details a few different functions the makefile is capable of. The clean-pyc rule locates all *.pyc, *.pyo or /*~ files and removes them from your directory. clean-build is for removing build artifacts. The isort executes an isort command using the string input detailed by the -c command. I'm going to be honest and admit I don't know what the function of lint is. test cleans out the directory by running clean-py before running a test.py file to test the program. docker-run builds and runs the docker. I changed the run rule into the default rule that way the script can be invoked with just 'make' instead of 'make run'. Phony at the beginning prevents the makefile from running a file called clean-pyc, if you had one. 
```sh
.PHONY: clean-pyc clean-build

HOST=127.0.0.1
TEST_PATH=./

clean-pyc:
    find . -name '*.pyc' -exec rm --force {} +
    find . -name '*.pyo' -exec rm --force {} +
   name '*~' -exec rm --force  {} 

clean-build:
    rm --force --recursive build/
    rm --force --recursive dist/
    rm --force --recursive *.egg-info

isort:
    sh -c "isort --skip-glob=.tox --recursive . "

lint:
    flake8 --exclude=.tox

test: clean-pyc
    py.test --verbose --color=yes $(TEST_PATH)


@If you only want to run this on a local machine, uncomment this and comment out the other run format.
@default:
@	python manage.py runsever

default:
    python manage.py runserver --host $(HOST) --port $(PORT)

docker-run:
    docker build \
      --file=./Dockerfile \
      --tag=my_project ./
    docker run \
      --detach=false \
      --name=my_project \
      --publish=$(HOST):8080 \
      my_project
```

## Java Makefile Template

A Simple Makefile Example: 
```sh
JCC = javac
OBJECTS = Name.class Name2.class [Insert all class files here]

# the -g flag compiles with debugging information
#
JFLAGS = -g

default: $(OBJECTS)

# these target entries build the Class files
# the Name.class file is dependent on the Name.java file
# and the rule associated with this entry gives the command to create it
#
Name.class: Name.java
        $(JCC) $(JFLAGS) Name.java

Name2.class: Name2.java
        $(JCC) $(JFLAGS) Name2.java

# Repeat for any remaining class files

clean: 
        $(RM) *.class
```
Notice this Makefile is capable of compiling multiple java files into the executable. Add/Alter the contents of the OBJECTS and JFLAGS for your program. For a list of javac flags, click [here](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javac.html). 

## Usage Example

Once you have created your Makefile, you should be able to use it from whichever directory it is stored in. Make sure your Makefile is in the same folder as all the files it requires.

To 'Make' the executable type:
```sh
make
```

To clean up the folder, removing all object, tar, and executable file types:
```sh
make clean
```

## Meta

Kenzie Clarke – [Linkedin Page](https://www.linkedin.com/in/kenzieclarke07/) – kenzieclarke@tcu.edu

Distributed under the GPL license. See ``LICENSE`` for more information.

[https://github.com/spinystarfish/github-link](https://github.com/spinystarfish)

## Contributing

1. Fork it (<https://github.com/yourname/yourproject/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request

## Special Thanks
Thank you to the following resources for information concerning the various Makefile examples.

[CS Department at College of Swarthmore](https://www.cs.swarthmore.edu/~newhall/unixhelp/howto_makefiles.html)

[GNU User's Guide for Native Platforms](https://gcc.gnu.org/onlinedocs/gnat_ugn/Interfacing-to-C.html)

[GNU User's Guide: Gnatmake](http://www.cs.fsu.edu/~baker/ada/gnat/html/gnat_ugn_7.html#SEC89)

.[Krzysztof Żuraw's Python Makefile](https://krzysztofzuraw.com/blog/2016/makefiles-in-python-projects.html)

<!-- Markdown link & img dfn's -->
[npm-image]: https://img.shields.io/npm/v/datadog-metrics.svg?style=flat-square
[npm-url]: https://npmjs.org/package/datadog-metrics
[npm-downloads]: https://img.shields.io/npm/dm/datadog-metrics.svg?style=flat-square
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat-square
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[wiki]: https://github.com/yourname/yourproject/wiki
