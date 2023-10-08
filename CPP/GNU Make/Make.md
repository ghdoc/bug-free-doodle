- Make (C++)

- [GNU Make - Table of Contents (mit.edu)](https://web.mit.edu/gnu/doc/html/make_toc.html#SEC4)

  

# GNU Make Udemy course  
    [https://github.com/cppbysubrat/makefile-udemy/tree/subrat-makefile](https://github.com/cppbysubrat/makefile-udemy/tree/subrat-makefile)

## Module 01  
    What happens behind the scenes when make executes and compilation results in an output binary? [Things To Remember](https://workflowy.com/#/455684c23dc3) 

	- Source code (sample.c) is fed to a preprocessor which renders a (sample.i) expanded source code i.e preprocessor generated file
	
	- For a cpp file like (sample.cpp) will generate (sample.ii)
	- All the #include directives and #ifdefs need to be processed during pre-processing. After that we get expanded source code.
	
	- Assembler will take that and generate (sample.s)
	- Compiler will read the .s file and generate a machine understandable object file (sample.o)
	- Linker will generate the executable by default a.out
	
	- you can also ask it to generate a named executable by providing -o flag and filename (sample)
	
	- When we run ./sample, the loader loads the binary a.out/sample into memory. Same steps are done for dynamic libs/static libs.

## Module 02

	- Possible Outputs
	
	- sample.cpp can generate:-
	
	- a.out (Binary Executable)
	- libSample.so (Shared object/dynamic library)
	
	- -shared flag
	- use lib prefix
	
	- sample.o -c flag created object code
	- libSample.a is a static library (using ar / rcs)
	
	- static libs are collection of one or more .o object files
	
	- How to create each output
	
	- sample.o => g++ -c sample.cpp -o sample.o
	- libSample.a => ar rcs libSample.a sample.o
	
	- ar=>Archive
	- rcs=> r=Replace old files, c=create if don't exist, s=>sort i.e. create a sorted indec of the library. sorting helps searching for functions inside the library
	
	- libSample.so => g++ -shared sample.cpp -o libSample.so
	- Output => g++ sample.cpp -o output

## Module 03

	- Project Folder Structure
	
	- src -> module-1,2,3,4,5
	- bins
	- libs
	- objs
	- sample-makefiles (templates for makefiles, std compilation flags etc, reusable stuff)
	- shared-headers
	- docs
	- experimental
	
	- module-1 generates a binary, which should go into bin
	- module-2 generates a shared object/dynamic library - should go into libs folder
	- module-3 uses dynamic lib from module-2. It should take it from libs folder. So we should keep headers of module-2 in shared-headers folder
	- Any experimental code during dev process should be kept in the experimental folder.
	- For production, we should give dynamic libs from libs folder. Static libraries are not needed because they are already inside our binaries


## Module 04

	- Make v/ Makefile
	
	- Makefile is same as makefile - both are valid
	- which make gives the location of our make binary
	- We use makefile to automate our build process.
	- make tells us which files have changed and recompile. It looks at the timestamp of source files and checks if target file time stamp is older. In that case it will build again, else not.
	
	- Structure of makefile
	
	- Comments
	- Macros/variables
	- Functions
	
	- Instructions/Statements  
	      
	
	- Similar to the main() in a c/cpp program, we have target in the make file.
	- Sample makefile  
	    VARIABLE 1
	- VARIABLE 2
	
	- define myfunction  
	-     ........  
	- endef
	
	- TARGET:PREREQUISITE/DEPENDENCY  
	-     INSTRUCTION-how to make/prepare the TARGET using prerequisites  
	- In makefile terminology, PREREQUISITES/DEPENDENCY is a Rule, and rest is a Recipe
	
	- Real world Makefile
	
	- First add a target  
	    TARGET:PREREQUISITE
	- INSTRUCTIONS-how to make/prepare the TARGET using PREREQUISITES
	- Target is followed by colon.
	- A target that is not really present is a Phony target. For example, clean.  
	    clean:
	- steps_to_cleanup (such as rm -rf *.bin)
	- .PHONY: clean
	- We may have other phony targets like downloading deps from packages. We can add another target called 'download_deps: download`  
	    .PHONY: clean download_deps
	- If we want to ignore error, then add a hyphen before the command in the make file
	
	- For example  
	    clear:
	-     rm f3.c
	
	- This would give an error if f3.c file didnot exist. So we instead run it like  
	    clear:
	-     -rm f3.c
	- and now we get this output: make clear  
	    rm f3.c
	- rm: cannot remove ‘f3.c’: No such file or directory
	- make: [clear] Error 1 (ignored)
	- Use a tab and not a space when entering INSTRUCTIONS on the line below the target
	
	- IMPORTANT POINTS
	
	- Makefile can have many targets
	- The first target is the DEFAULT target
	- Use .DEFAULT_GOAL to override it
	
	- .DEFAULT_GOAL={default_target_name}

## Module 05

	- Go to [Module 05](https://workflowy.com/#/f289b3689c20) 
	
	- Build only when source code changes
	
	- We want to do incremental builds on our make file below:  
	    default:
	-     gcc mod1.c -o ../../bins/mod1
	
	- Add variables to simplify the makefile  
	    OUTPUT = ../../bins/mod1
	- INPUT = mod1.c
	- $(OUTPUT) :
	-     gcc $(INPUT) -o $(OUTPUT)
	- Simplify further by using shortforms for target and inputs
	
	- $(<) gives first dependency
	- $(^) gives all dependencies
	- $(@) is same as $@ because it is only one character, so no parenthesis needed
	
	- simplified makefiel  
	    OUTPUT = ../../bins/mod1
	- INPUT = mod1.c
	- $(OUTPUT) : 
	-     gcc $< -o $@
	
	- Add support for objs
	
	- -c generates the object file  
	    OUTPUT = ../../bins/mod1
	- INPUT = mod1.c
	- $(OUTPUT) : $(OBJ1)
	-     gcc $< -o $@
	- $(OBJ1) : $(INPUT)
	-     gcc -c $< -o $@
	
	- Add support for dependencies
	
	- mod1 source depends on math.h library So we need to add that to our make file when we are generating the binary using -lm where  
	    OUTPUT = ../../bins/mod1
	- INPUT = mod1.c
	- $(OUTPUT) : $(OBJ1)
	-     gcc $< -o $@ -lm
	- $(OBJ1) : $(INPUT)
	-     gcc -c $< -o $@
	
	- Why we don't need linker flag for <stdio.h>
	
	- For <math.h> we need to use -lm to make our makefile linker independent In man sqrt you will see that we are asked to use -lm
	
	- How to enable Warnings
	
	- Use -Wall where we create obj file. Here W = Warning & all is all warnings.  
	    $(OBJ1) : $(INPUT)
	-     gcc -Wall -c $< -o $@
	
	- Treat warnings as errors
	
	- Use -Werror to treat all warnings as errors.a
	- New Make file
	
	- Add Linker flag and compiler flags  
	    OUTPUT = ../../bins/mod1
	- INPUT = mod1.c
	- OBJ1= ../../objs/mod1.o
	- CFLAGS = -Wall -Werror
	- LDFLAGS = -lm
	
	- $(OUTPUT) : $(OBJ1)
	-     gcc $< -o $@ $(LDFLAGS)
	- $(OBJ1) : $(INPUT)
	-     gcc $(CFLAGS) -c $< -o $@
	
	- Go to [Module 06](https://workflowy.com/#/cec03ecc9f96) 

## Module 06

	- Go to [Module 06](https://workflowy.com/#/cec03ecc9f96) 
	
	- Organize Makefile in better way  
	    MODULE_NAME = mod1
	
	- TARGET_DIR = ../../bins
	- TARGET_NAME = mod1_bin
	- TARGET = $(TARGET_DIR)/$(TARGET_NAME)
	
	- OBJ_DIR = ../../objs
	- OBJ1 = $(OBJ_DIR)/$(MODULE_NAME).o
	
	- CFLAGS = -Wall -Werror
	- LDFLAGS = -lm
	
	- $(TARGET) : $(OBJ1)
	-     gcc $< -o $@ $(LDFLAGS)
	- $(OBJ1) : $(MODULE_NAME).cpp
	-     gcc $(CFLAGS) -c $< -o $@
	
	- clean:
	-     rm $(TARGET) $(OBJ1)
	- Requirements for Project
	
	- mod1 - Binary
	- mod2 - Dynamic (.so)
	- mod3 - Binary uses Dynamic lib .so from mod2
	- mod4 - Static lib (.a)
	- mod5 - Binary uses Dynamic lib .so from mod2 and static lib .a from mod4
	
	- Makefile for module 4 (remember [Requirements for Project](https://workflowy.com/#/7b2fe02f833a) )

	- Go to [Module 07](https://workflowy.com/#/3221929f39fb) 

## Module 07

- Module 3 - Binary (Uses Dynamic Lib .so from Mod2)

- Compiling a shared object

- use -shared flag
- use -fPIC (needed for gcc/g++, not for CLANG) for position independant code
- we add code for mod2.h & mod2.cpp and test_mod2.cpp to execute funcn in mod2. But we get this error on running g++ test_mod2.cpp  
    g++ test_mod2.cpp
- test_mod2.cpp: In function ‘int main()’:
- test_mod2.cpp:4:19: error: ‘fun2’ was not declared in this scope
- int main() { fun2(); }
-                   ^
- So we have to provide correct flags - gcc test_mod2.cpp -L. -lmod2 Here -L. means library is located here "." and -l means library mod2 is used
- Problems on compilation  
    >gcc test_mod2.cpp -L. -lmod2

- ./[libmod2.so](http://libmod2.so/): undefined reference to `std::ostream::operator<<(std::ostream& (*)(std::ostream&))'
- ./[libmod2.so](http://libmod2.so/): undefined reference to `std::basic_ostream<char, std::char_traits<char> >& std::endl<char, std::char_traits<char> >(std::basic_ostream<char, std::char_traits<char> >&)'
- ./[libmod2.so](http://libmod2.so/): undefined reference to `std::cout'
- ./[libmod2.so](http://libmod2.so/): undefined reference to `std::basic_ostream<char, std::char_traits<char> >& std::operator<< <std::char_traits<char> >(std::basic_ostream<char, std::char_traits<char> >&, char const*)'
- ./[libmod2.so](http://libmod2.so/): undefined reference to `std::ios_base::Init::~Init()'
- ./[libmod2.so](http://libmod2.so/): undefined reference to `std::ios_base::Init::Init()'
- collect2: error: ld returned 1 exit status
- This happens because we used gcc instead of g++ This error can be solved by using the g++ command instead of gcc to compile the program1. The g++ command automatically links the C++ standard library with your program.

- Module 3 makefile  
    MODULE_NAME = mod2
- TEST_MODULE_NAME = test_mod2
- TEST_MODULE = $(TEST_MODULE_NAME).cpp

- TARGET_DIR = ../../libs
- TARGET_NAME = lib$(MODULE_NAME).so
- TARGET = $(TARGET_DIR)/$(TARGET_NAME)

- TEST_BIN_DIR = ../../test_build

- OBJ_DIR = ../../objs
- OBJ1 = $(OBJ_DIR)/$(MODULE_NAME).o

- CFLAGS = -fPIC -Wall -Werror
- LDFLAGS =

- $(TARGET) : $(OBJ1)
-         g++ -shared $< -o $@ $(LDFLAGS)
- $(OBJ1) : $(MODULE_NAME).cpp
-         g++ $(CFLAGS) -c $< -o $@

- test:
-         g++ $(TEST_MODULE) -o $(TEST_BIN_DIR)/$(TEST_MODULE_NAME) -L$(TARGET_DIR) -l$(MODULE_NAME)
- clean:
-         rm $(TARGET) $(OBJ1)

- build_dir:
-         mkdir -p $(TEST_BIN_DIR)
- How to make shared_headers available for including without path

- we should know this detail at compile time
- it should be a part of compilation flag
- INC_PATH = ../../share_headers
- CFLAGS = $(INC_PATH)

- Go to [Module 08](https://workflowy.com/#/8ab46cff8bec) 

## Module 08

- Makefile for module 4 (remember [Requirements for Project](https://workflowy.com/#/7b2fe02f833a) )
- In here we use "ar rcs" to generate the .a file  
    $(TARGET) : $(OBJ1)
-         ar rcs $@ $^

- $(TARGET) : $(OBJ1)

- ar rcs $@ $^
- Here $@ is the target and $^ is the obj
- All the obj should be archived to the target (libmod4.a)

- Makefile mod4  
    MODULE_NAME = mod4
- TEST_MODULE_NAME = test_$(MODULE_NAME)
- TEST_MODULE = $(TEST_MODULE_NAME).cpp
- TEST_BIN_DIR = ../../test_build

- TARGET_DIR = ../../libs
- TARGET_NAME = lib$(MODULE_NAME).a
- TARGET = $(TARGET_DIR)/$(TARGET_NAME)

- OBJ_DIR = ../../objs
- OBJ1 = $(OBJ_DIR)/$(MODULE_NAME).o

- CFLAGS = -fPIC -Wall -Werror
- LDFLAGS =

- $(TARGET) : $(OBJ1)
-         ar rcs $@ $^
- $(OBJ1) : $(MODULE_NAME).cpp
-         g++ $(CFLAGS) -c $< -o $@
- test:
-         g++ $(TEST_MODULE) -o $(TEST_BIN_DIR)/$(TEST_MODULE_NAME) -L$(TARGET_DIR) -l$(MODULE_NAME)
- clean:
-         rm $(TARGET) $(OBJ1)

- build_dir:
-         mkdir -p $(TEST_BIN_DIR)

## Module 09

- Mod5 - binary that uses dynamic lib .so and static lib .a

- Makefile  
    MODULE_NAME = mod5

- TARGET_DIR = ../../bins
- TARGET_NAME = $(MODULE_NAME)_bin
- TARGET = $(TARGET_DIR)/$(TARGET_NAME)

- OBJ_DIR = ../../objs
- OBJ1 = $(OBJ_DIR)/$(MODULE_NAME).o

- INC_PATH = ../../share_headers
- WARN_FLAGS = -Wall -Werror
- CFLAGS = $(WARN_FLAGS) -I$(INC_PATH)

- LIBS_PATH = ../../libs/
- LDFLAGS = -L$(LIBS_PATH) -lmod2 -lmod4

- $(TARGET) : $(OBJ1)
-         g++ $< -o $@ $(LDFLAGS)
- $(OBJ1) : $(MODULE_NAME).cpp
-         g++ $(CFLAGS) -c $< -o $@

- clean:
-         rm $(TARGET) $(OBJ1)


## Module 10

### Things To Remember

- #todo read about optimization flags

- Module 01  
    What happens behind the scenes when make executes and compilation results in an output binary? [Things To Remember](https://workflowy.com/#/455684c23dc3) 

- What about passing a MACRO from outside the program
- Say we have a code like below macro.cpp:  
    #include <stdio.h>

- int main()
- {
- printf("%s\n", MY_NAME);
- }
- It doesn't have a constant or macro defined in the code. But we can provide one from the outside as follows:
- gcc -DMY_NAME=\"SOME_STRING\" macro.cpp

- -D means "Define" followed by Macro name
- \" will be replaced by a single "

- Introduction to -std flag
- It allows to select the C++ standard. In our makefile/g++ command, we specify -std=c++11 or c++14 or...
- g++ -std=c++2a demo.cpp where 2a => c++ 20
- Difference between = & :=
- Lazy => =
- Instant => :=
- Makefile with error  
    var1=10
- var2=20
- var3=40

- var1=$(var1) 10000

- default:
-         echo $(var1)

- Here we get this error: make

- makefile:5: *** Recursive variable `var1' references itself (eventually).  Stop.
- This is because make executes this in an infinitely recursive/reentrant loop i.e. simultaneously initialize var1 while also getting its value

- So we change it to **var1:=$(var1) 10000**

- PHONY target
- Sometime we have a file with the same name as a target. In the example below, there is a file named default, which is also a target in our make file. So we define the target as PHONY => .PHONY: default  
    var1=10
- var2=20
- var3=40

- var1=$(var1) 10000
- .PHONY: default
- default:
-         echo $(var1)
- Go to [Module 11](https://workflowy.com/#/6bda2ee4872f) 

## Module 11

- Makefile Template
- How to add cross compilation feature
- Better way to accessing bins/libs/shared headers
- Copying of headers to shared  headers during building of .so & .a

- There are two kinds of build: DEBUG and RELEASE
- #ref:linux:flags [https://linuxhandbook.com/gcc-flags/](https://linuxhandbook.com/gcc-flags/)
- Templated Makefile  
      1 # Lazy init with =, means whenever the var is used, only then
-   2 # it will be evaluated
-   3 BUILD_TYPE = $(RELEASE)
-   4 #BUILD_TYPE = $(DEBUG)
-   5
-   6 MODULE_NAME =
-   7 TARGET_NAME =
-   8
-   9 PROJ_ROOT_DIR = ../..
-  10 OBJ_DIR = $(PROJ_ROOT_DIR)/objs/$(MODULE_NAME)
-  11
-  12 #****DON'T MODIFY BELOW ATTRIBUTES****
-  13 # this is a macro that can be used in our program
-  14 # we can write in our app logs when the binary was generated
-  15 BUILD_TIMESTAMP = $(shell date + '%d-%m-%Y.%H-%M-%S.%N')
-  16
-  17 # here we capture a env var named INSTALLATION_PATH by
-  18 # echo and saving into a var also called as INSTALLATION_PATH
-  19 # usually we use export INSTALLATION_PATH=/usr/local/bin
-  20 INSTALLATION_PATH = $(shell echo $$INSTALLATION_PATH)
-  21 ifeq ($(INSTALLATION_PATH),)
-  22         INSTALLATION_PATH = $(PROJ_ROOT_DIR)
-  23 #       INSTALLATION_PATH = /usr/local/mycustombuild
-  24 endif
-  25
-  26 # We are able to configure where bins and libs
-  27 # should be saved as below.
-  28 TARGET_DIR = $(INSTALLATION_PATH)/bins
-  29 TARGET = $(TARGET_DIR)/$(TARGET_NAME)
-  30
-  31 LIBRARY_DIR = $(INSTALLATION_PATH)/libs
-  32
-  33 # Cross compilation
-  34 #
-  35 # C++ Compiler
-  36
-  37 CXX = $(shell echo $$CXX)
-  38 # if c++ compiler is not set, then use g++
-  39 ifeq ($(CXX),)
-  40 CXX = g++
-  41 endif
-  42
-  43 # C++ Linker
-  44 # Good idea to separate compiler and linker
-  45
-  46 LDXX = $(shell echo $$CXX)
-  47 ifeq ($(LDXX),)
-  48 LDXX = g++
-  49 endif
-  50
-  51 STDFLAG = -std=c++17
-  52
-  53 #*****DON'T MODIFY BELOW ATTRIBUTES****
-  54 MAIN_OBJ = $(OBJ_DIR)/main.o
-  55
-  56 SOURCE_1 = $(MODULE_NAME)
-  57 OBJ_1 = $(OBJ_DIR)/$(SOURCE_1).o
-  58
-  59 # MAY NEED TO ADD MORE DEPS AS PER REQUIREMENTS.\
-  60 # 1. DONT ADD EXTENSION C/CPP AS IT MAKES EASIER TO CREATE .o FILE OTHERWISE
-  61 # IT WILL CREATE *.cpp.o WHICH IS OK!
-  62 # 2. ADD *.o IN ALL_OBJS
-  63 # 3. ADD INSTRUCTIONS TO BUILD TARGET (.o)
-  64
-  65 # ADd OBJ_* IN THE BEGINNING IF REQUIRED
-  66 ALL_OBJS = $(OBJ_1) $(MAIN_OBJ)
-  67
-  68 # WE need this to point where to get shared headers from
-  69 INC = -I./ -I$(PROJ_ROOT_DIR)/share_headers
-  70
-  71 # choose release/debug
-  72 # In DEBUG we have lots of symbols.
-  73 DEBUG = -pipe -g -Wall -W -fPIC
-  74 #RELEASE = -DNDEBUG -W -fPIC
-  75 RELEASE = -pipe -O2 -Wall -W -fPIC
-  76
-  77 # -D stands for DEFINE. If you want to define any macro which
-  78 #  is used in code for timestamp or git revision etc.
-  79 DEFINES = -DBUILD_TIMESTAMP_STR=\"$(BUILD_TIMESTAMP)\" \
-  80         -DINSTALLATION_PATH_STR=\"$(INSTALLATION_PATH)\"
-  81
-  82 # If you want optimization during linking time, then you can enable below
-  83 #LD_OPT = -Wl,-01
-  84
-  85 # UNCOMMENT IF YOU LIKE TO SEE FOLLOWING WARNINGS. ATLEAST ONCE THIS NEEDS
-  86 # TO BE RUN FOR EACH MODULE
-  87
-  88 WARN = -Wall -Wextra -Werror -Wwrite-strings -Wno-parentheses - pedantic \
-  89         -Warray-bounds -Wno-unused-variable -Wno-unused-functions \
-  90         -Wno-unused-parameter -Wno-unused-result
-  91
-  92 # Compilation flags
-  93 CCFLAGS = $(STDFLAG) $(BUILD_TYPE) $(DEFINES) $(WARN) $(INC)
-  94
-  95 # Add dependency library here by separating them with space.
-  96 # Below example is to add libzmq, libm & libcustomlib
-  97
-  98 # Note: Add the "<path to library> -llibraryname" by keeping space in between as shown below \
-  99 # if library is present in the current directory, we can use path as L.
- 100
- 101 # DEP_LIBS = -lzmq -lm -L$(LIBRARY_DIR) -lcustomlib -L. -lnewlibincurrentdir
- 102
- 103 # When we use dynamic library, then at runtime, the program/binary
- 104 # needs to find that library in pre-defined path. If not found at runtime,
- 105 # our program won't run. Usually we use LD_LIBRARY_PATH.
- 106
- 107 # RPATH IS USED FOR LINKING LIBS IN SPECIFIC PATH
- 108 # RPATH="-Wl, -rpath, $(LIBRARY_DIR):$(THIRD_PARTY_LIB_DIR)"
- 109 # Linker will search in RPATH
- 110 RPATH="-Wl,-rpath,$(LIBRARY_DIR)"
- 111
- 112 # LDFLAGS = $(DEBUG) $(PROF) -L$(LIBRARY_DIR) -L$(THIRD_PARTY_LIB_DIR) -fPIC \
- 113 #       -lpthread $(DEP_LIBS) $(RPATH)
- 114
- 115 LDFLAGS = $(DEP_LIBS) $(RPATH)
- 116
- 117 # all is our first target. So it will be the first target for make
- 118 all: $(TARGET)
- 119
- 120 $(TARGET: $(ALL_OBJS)
- 121         $(LDXX) $(LD_OPT) -o $@ $^ $(LDFLAGS)
- 122
- 123 $(MAIN_OBJ): main.cpp
- 124         $(CXX) $(CCFLAGS) -o $@ -c $<
- 125
- 126 $(OBJ_1): $(SOURCE_1).cpp
- 127         $(CXX) $(CCFLAGS) -o $@ -c $<
- 128
- 129 # $(OBJ_2): $(SOURCE_2).cpp
- 130 #       $(CXX) $(CCFLAGS) -o $@ -c $<
- 131
- 132 # @echo where @ will suppress printing echo word on console.
- 133 build_dir:
- 134         @echo Creating object director if not exist
- 135         mkdir -p $(OBJ_DIR)
- 136
- 137 clean:
- 138         @echo Clean build
- 139         -rm $(ALL_OBJS)
- 140         -rm $(TARGET)
- 141
- 142 .PHONY: clean build_dir all
- 143

- Go to [Module 11](https://workflowy.com/#/6bda2ee4872f) 

- Go to [Module 12](https://workflowy.com/#/2ea9b500ff42) 

## Module 12

- Go to [Module 12](https://workflowy.com/#/2ea9b500ff42)