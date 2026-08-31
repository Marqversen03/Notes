
it is a standalone tool that automates the compile process

### CI CD


### Dokumentation
makefioles can make documentation from comments, this makes every task more streamlines. comment each function and what it does. make a standart author and date at the top of the code.


### GNU MAKEfile
a build system is make og specificly GNU make
it compiles the code for you. you just run a makefile and it sorts it for u. aslong as u set up the file correct

**Compiler**
g++ is  the latest compiler installed on the system. this is important when making code over long period the compiler can change and it can fuck something up so defining it to g++ 12 for example then it will keep being g++ 12 version. if that is installed. 

### Basics

There are 3 main funktion in a makefile
##### Target
Actions or tasks to be performed, such a compiling source code, linking binaries, cleaning directories, or running tasks
##### Dependencies
files or conditions that must bee satisfied before executing a target. this one is really importing for scaling software. it will check if updates are made og running task already qualify. this makes scaling less hard for the system. every running task has a running date

##### Commands
shell commands or scripts associated with each target, defining how to accomplish the task



#### Structure

when compiling it reads from top down but if it finds a line that is dependend on a later line it wille run through and come back. this is importent when looking at libs

`````c++
Target:dependencies
	command
	command
`````


`````c++
hello.out : hello.cpp
	g++ hello.cpp -o hello.out
`````

this is a easy struckture. it starts knowing the target hello.out. meaning it knows it needs a final of hello.out it has the dependency og the hello.cpp so first thing it does is to check if the hello.out exist. if it does it compares the file date to the dependencie of hello.cpp if does match logic distakes that hello.out is up to date and it does nothing. if they do not. hello.cpp has been changes. then it runs the command to run the command g++ hel...

##### Obj
A obj file like hello.o is not a source code it is an object file that contains the code
**does it contain the libs? i think not**


### Questions
hva forskellen på hello.o og hello.obj


###  Advanced Makefile

to make it more streamlined we use macro definition. here we just use the equal sign.

#### $@
Macro with @ refering to target
`````c++
hello.out: hello.o greeting.o
	g++ $< -o $@
`````
here it the end is refering to the target. wich states that the hello.out target is the same as the output of the command
#### $<
Macro with @ refering to frist dependancy
`````c++
hello.out: hello.cpp greeting.h
	g++ $< -o $@
`````
here we use the $< to refere to the first dependancy. so we state that the file it needs to make the out file is the dependancy
#### $^
Macro with @ refering to all dependencies
`````c++
hello.out: hello.cpp greeting.h
	g++ $^ -o $@
`````
Same concept here we just state all dependancy so it needs to create it from hello.cpp and greeting.h **HOW THE FUCK**

#### *
this is a joker, it can represent all char. so if i search ban*o in a directory of cool words itt will show (banjo, bando, banko) you could also say like remove files with the name *.o then it deletes all files with the .o 

#### %.o


`````c++
CXX = g++ 
Header = greeting.h

hello.out: hello.o greeting.o
	$(CXX) $^-o $@
	
%.o: %.cpp $(Header)
	$(CXX) -c $< -o $@
`````


#### Lib
A standert for linux is all libary files a called lib and the somethig and the o or so:
`````c++
libX.o 
libX.so
`````
when making lib files whe need to place them in /bin/lib/
then any user can use it in any software.
when copying a file to lib we need to do sudo. couse it is a protected ditectory

to copy a lib file to the lib use this command. where it copy the objekt file and defines it as a .a file
`````c++
sudo cp greeting.o /usr/lib/libGreeting.a
`````

to include a lib to a makefile we define LDFLAGS here we can define with libs we want to include. to do so we add the name with with lib removed and replaced just with l. so lgreeting or lmath or lstring. when compiling we define cxxflags this just is a compiling definition. that states we want more infomation. here we write Wall with stands for warning all. so we want all warning even if the warning doesnt make to program fail.
`````c++
CXXFLAGS = -Wall
LDFLAGS = -l...
`````

to include it we write it likes this. defining we want to flags and libs
`````c++
hello.out: hello.o
	$(CXX) $(CXXFLAGS) $(LDFLAGS) $^ -o $@
`````



#### Standart Makefile targets

#### All
this target holds all the program needs to run.
#### Install
compile the program and copy the executables, libs etc. it should have simple test to verify that a prgrams is properly runs
#### Clean
delete all object files and executable files that are normally created in the current directory

### Why
we want our code to be as lean as posible. to make the code less system depended. to do so we need it only to use memory when it is needed for code. to do so we make the code use object files or libs. speed isnt a problem the real problem is memory. ram is always gonna fill and be expensive. so when coding ensure memory is kept as small as possible. speed is only really a focus when looking at searcing algorithm or streaming. 



`````c++
CXX = g++   // Compiler used
CXXFLAGS = -Wall -Wextra -std=c++17  
TARGET = program  
SRCS = main.cpp  // tilføj alle cpp filer der bruges
OBJS = $(SRCS:.cpp=.o)  

all: $(TARGET)  

$(TARGET): $(OBJS)  

$(CXX) $(OBJS) -o $(TARGET)  

%.o: %.cpp  

$(CXX) $(CXXFLAGS) -c $< -o $@  

run: $(TARGET)  

./$(TARGET)  

clean:  

rm -f $(OBJS) $(TARGET)  

rebuild: clean all  

.PHONY: all run clean rebuild
`````

