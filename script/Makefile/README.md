# Makefile

**빌드를 간편**하게 할 수 있는 script file이다.
> bash 명령어는 아니다.

## Contents		
* ### [GCC](https://github.com/mingeun2154/skill/tree/main/script/Makefile#gcc-1)
* ### [Make](https://github.com/mingeun2154/skill/tree/main/script/Makefile#make-1)
* ### [Makefile](https://github.com/mingeun2154/skill/tree/main/script/Makefile#makefile-2)
* ### [예시](https://github.com/mingeun2154/skill/tree/main/script/Makefile#example)      

#    

## GCC

### 소개
GNU 프로젝트의 일부로 개발되어 널리 쓰이고 있는 컴파일러이다. 
> GNU는 운영체이다.

처음에는 GNU C Compiler였지만 1999년 이후부터 다양한 언어를 지원하게 되었다. 지금은 GNU Compiler Collection이라고 한다.

`C/C++`, `Objective-C`, `Fortran`, `Ada`, `Java` 등을 지원한다.

일반적으로 GCC를 컴파일러라고 하지만, 정확히는 소스파일을 이용하여 **실행 파일을 만들 때까지 필요한 프로그램을 차례로 실행**하는 툴이다.
> 전처리기, compiler, assembler, linker를 차례로 실행한다.

### 명령어 옵션

* `-c` : 소스파일을 오브젝트 파일로만 변환하고, 링크는 하지 않는다.
* `-o` : 바이너리 형식 출력 파일 이름을 지정할 때 사용한다. 지정하지 않으면 a.out으로 생성된다.       
		`$ gcc -o [출력파일 이름] [소스파일 이름]`       
		`$ gcc [소스파일 이름] -o [출력파일 이름]`        
* `-I` : 헤더파일을 검색하는 디렉토리 **목록**(배열)을 추가한다. System search path에 등록되지 않은 경로의 헤더 파일을 찾는다.
* `-S` : 소스파일을 어셈블리 파일로만 컴파일한다.
* `-E` : 소스파일을 전처리 단계까지만 처리한다.
* `-L` : 라이브러리 파일을 검색하는 디렉토리 **목록**을 추라한다.
* `-l` : 라이브러리 파일(오브젝트 파일)을 링크한다. 라이브러리는 확장자를 제외한 파일 이름만 명시한다. (dynamic linking)
* `-g` : 바이너리 파일에 표준 디버깅 정보를 포함한다.
* `-ggdb` : 바이너리 파일에 GNU 디버거인 GDB만 이해할 수 있는 다양한 디버깅 정보를 포함한다.
* `-O [level]` : 컴파일 코드를 최적화 하며, 최적화 level을 지정한다. (1~3)
* `-D[FOOl=[BAR]` : command line에서 BAR 값을 가지는 FOO라는 매크로를 정의한다.
* `static` : 정적 라이브러리에 링크
* `-MM` : make 호환의 의존성 목록을 출력한다.
* `-V` : 각 단계에서 사용되는 명령을 보여준다. (전처리, 컴파일, 어셈블, 링크)

## Make
수정된 소스 파일만 찾아내 컴파일, 어셈블하고 수정되지 않은 파일들은 기존 오브젝트 파일을 그대로 이용하게 해주는 utility tool이다.

cli에서 `$ make`를 입력하면 Makefile에 정의된 루틴이 실행되어 실행파일이 만들어진다.

## Makefile
Makefile을 구성하는 요소는 다음과 같다. 이 셋을 하나의 **element**라고 한다면, 그 **순서는 중요하지 않다.**

* Target : 명령어 실행으로 생성할 대상(파일)
* Dependency : 의존하는 파일
* Command : target을 생성하기 위한 명령어
	>명령은 반드시 tab으로 시작해야 한다.

```Makefile
main.out : main.c
	gcc -o main.out main.c
```

### 내부 매크로(변수)
Makefile을 작성할 때 사용하면 편한 변수들이다. 값들이 내부적으로 결정되어 있다. 그냥 사용하면 된다.

* `$@` : 현재 target의 이름
* `$*` : 확장자를 제외한 현재 target의 이름
* `$<` : 현재 dependency들 중 첫 번째 파일의 이름
* `$?` : 현재 target보다 최근에 변경된 dependency 이름
* `$^` : 현재 모든 dependencies

그 외에 필요하다면 변수(매크로)를 만들어서 사용할 수 있다.

## Example

[OpenGL과 glfw](https://github.com/mingeun2154/CS/tree/main/CG/DevEnv#opengl-and-glu)를 이용한 프로그램을 빌드하기 위한 Makefile이다.

```Makefile
CC = g++

# glfw header file search path
INC = -I/opt/homebrew/Cellar/glfw/3.3.8/include 
# .dylib path (glfw dynamic library version)
LIBS = -L/opt/homebrew/Cellar/glfw/3.3.8/lib
LIB_NAME = -lglfw
FRAMEWORK = -framework OpenGL

OBJS = p01_prep.o glSetup.o
SRCS = p01_prep.cpp glSetup.cpp

# executable file name
TARGET = p01_prep

$(TARGET) : $(OBJS)
	$(CC) $(LIBS) -o $(TARGET) $(OBJS) $(FRAMEWORK) $(LIB_NAME)

p01_prep.o : p01_prep.cpp
	$(CC) -c $< $(INC)

glSetup.o : glSetup.cpp
	$(CC) -c $< $(INC)

clean : 
	rm -rf $(OBJS)
```
