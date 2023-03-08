# Report-03

# Task 1

Вам поручили перейти на систему автоматизированной сборки CMake. Исходные файлы находятся в директории `formatter_lib`. В этой директории находятся файлы для статической библиотеки `formatter`. Создайте `CMakeList.txt` в директории `formatter_lib`, с помощью которого можно будет собирать статическую библиотеку formatter

```
$ echo "# lab-03" >> README.md
$ git init
$ git add README.md
$ git commit -m "fork"
$ git remote add origin https://github.com/ledibonibell/lab-03.git
$ git push -u origin master
```
```
$ git checkout -b lab
$ cat >> CMakeLists.txt << EOF
> EOF
$ nano CMakeLists.txt
```

Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(formatter)

add_library(formatter STATIC formatter.cpp)
target_include_directories(formatter PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```

```
$ git add CMakeLists.txt
$ git commit -m "added CMakeLists.txt"
$ git push origin master
$ git add formatter.cpp
$ git commit -m "added formatter.cpp"
$ git push origin lab
```

```
$ cmake -H. -B_build
$ cmake --build _build
```

# Task 2

# Task 3
