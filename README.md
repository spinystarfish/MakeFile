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
Insert Template Here
```
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
The -o option specifies the name of the executable file. To have the name of the executable be different from the program name, simply replace the $(TARGET) after -o on line 6 to the name you desire. Please Note that this Makefile does use the GCC compiler along with gnatmake

## C Makefile Template

## Python Makefile Template

## Java Makefile Template

## Usage example

Once you have created your Makefile, you should be able to use it from whichever directory it is stored in. Make sure your Makefile is in the same folder as all the files it requires.

To 'Make' the executable type:
```sh
make
```
To clean up the folder, removing all object, tar, and executable file types:
```sh
make clean
```

![](header3.jpg)

## Meta

Kenzie Clarke – [Linkedin Page](https://www.linkedin.com/in/kenzieclarke07/) – kenzieclarke@tcu.edu

Distributed under the MIT license. See ``LICENSE`` for more information.

[https://github.com/spinystarfish/github-link](https://github.com/spinystarfish)

## Contributing

1. Fork it (<https://github.com/yourname/yourproject/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request

<!-- Markdown link & img dfn's -->
[npm-image]: https://img.shields.io/npm/v/datadog-metrics.svg?style=flat-square
[npm-url]: https://npmjs.org/package/datadog-metrics
[npm-downloads]: https://img.shields.io/npm/dm/datadog-metrics.svg?style=flat-square
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat-square
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[wiki]: https://github.com/yourname/yourproject/wiki
