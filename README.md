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
![Снимок экрана от 2023-03-05 20-55-15](https://user-images.githubusercontent.com/125737299/224361461-a5d9477e-4dbb-48c2-829e-d072f7cedf1c.png)

```
$ git checkout -b lab
$ cat >> CMakeLists.txt << EOF
> EOF
$ nano CMakeLists.txt
```
![Снимок экрана от 2023-03-05 21-17-14](https://user-images.githubusercontent.com/125737299/224361910-710dbb09-fc8f-419e-b907-10640e09ec80.png)


Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(formatter)

add_library(formatter STATIC formatter.cpp)
target_include_directories(formatter PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```

- Команда cmake_minimum_required указывает подходящую минимальную версию Cmake
- Команды set(CMAKE_CXX_STANDARD 11), set(CMAKE_CXX_STANDARD_REQUIRED ON) устанавливают значения стандартных переменных в Cmake(в данном случае CMAKE_CXX_STANDARD и CMAKE_CXX_STANDARD_REQUIRED)
- Команда project(formatter) создает проект formatter, к которому можно подключать библиотеки, исполняемы файлы и т.д.
- Команда add_library(formatter STATIC formatter.cpp) создает статическую библиотеку из указываемых файлов
- Команда target_include_directories связывает библиотеку formatter и CMAKE_CURRENT_SOURCE_DIR

```
$ git add CMakeLists.txt
$ git commit -m "added CMakeLists.txt"
$ git push origin lab
$ git add formatter.h
$ git commit -m "added formatter.h"
$ git push origin lab
$ git add formatter.cpp
$ git commit -m "added formatter.cpp"
$ git push origin lab
```

Проверяем работоспособность CMake:
```
$ cmake -H. -B_build
$ cmake --build _build

```
![Снимок экрана от 2023-03-05 21-58-59](https://user-images.githubusercontent.com/125737299/224361992-cb7e3ed2-1250-4eed-bb53-e241bad02662.png)


# Task 2

У компании "Formatter Inc." есть перспективная библиотека, которая является расширением предыдущей библиотеки. Т.к. вы уже овладели навыком созданием `CMakeList.txt` для статической библиотеки formatter, ваш руководитель поручает заняться созданием `CMakeList.txt` для библиотеки formatter_ex, которая в свою очередь использует библиотеку formatter

```
$ cat >> CMakeLists.txt << EOF
> EOF
$ nano CMakeLists.txt
```
![Снимок экрана от 2023-03-05 22-42-31](https://user-images.githubusercontent.com/125737299/224362290-cb605474-9e22-4322-836e-fc1f837e5bf0.png)

Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(formatter_ex)

add_library(formatter_ex STATIC formatter_ex.cpp)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter)
target_include_directories(formatter_ex PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_link_libraries(formatter_ex formatter)
```

- Команда add_subdirectory(../formatter_lib formatter) включает в сборку директорию с библиотекой formatter
- Команда target_link_libraries(formatter_ex formatter) связывает библиотеку formatter с formatter_ex
- Остальные команды аналогичны первому заданию

```
$ git add CMakeLists.txt
$ git commit -m "added CMakeLists.txt"
$ git push origin lab
$ git add formatter_ex.h
$ git commit -m "added formatter_ex.h"
$ git push origin lab
$ git add formatter_ex.cpp
$ git commit -m "added formatter_ex.cpp"
$ git push origin lab
```

Проверяем работоспособность CMake:
```
$ cmake -H. -B_build
$ cmake --build _build
![Снимок экрана от 2023-03-05 22-42-42](https://user-images.githubusercontent.com/125737299/224362332-43b22a5a-dd87-430c-8966-0ccf0f8f0f96.png)
![Снимок экрана от 2023-03-05 23-05-50](https://user-images.githubusercontent.com/125737299/224362500-d694c5a9-146f-4683-a8a4-9d91d854ad6e.png)
```

# Task 3
Конечно же ваша компания предоставляет примеры использования своих библиотек. Чтобы продемонстрировать как работать с библиотекой `formatter_ex`, вам необходимо создать два `CMakeList.txt` для двух простых приложений:

- `hello_world`, которое использует библиотеку `formatter_ex`;
- `solver`, приложение которое испольует статические библиотеки `formatter_ex` и `solver_lib`

Удачной стажировки!

### solver.cpp

```
$ cat >> CMakeLists.txt << EOF
> EOF
$ nano CMakeLists.txt
```
![Снимок экрана от 2023-03-05 23-06-08](https://user-images.githubusercontent.com/125737299/224362765-7babfae7-4d63-4e3d-9343-9a2cd2f31944.png)


Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(solver_lib)

add_library(solver_lib STATIC solver.cpp)
target_include_directories(solver_lib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```

- Команды аналогичны заданию 2 и 3

```
$ git add CMakeLists.txt
$ git commit -m "added CMakeLists.txt"
$ git push origin lab
$ git add solver.h
$ git commit -m "added solver.h"
$ git push origin lab
$ git add solver.cpp
$ git commit -m "added solver.cpp"
$ git push origin lab
```

Проверяем работоспособность CMake:
```
$ cmake -H. -B_build
$ cmake --build _build
```
![Снимок экрана от 2023-03-05 23-05-50](https://user-images.githubusercontent.com/125737299/224362629-6e8ca75a-434f-4ebd-a7a7-d812549c6fb7.png)


### solver_example

```
$ cat >> CMakeLists.txt << EOF
> EOF
$ nano CMakeLists.txt
```
![Снимок экрана от 2023-03-05 23-16-30](https://user-images.githubusercontent.com/125737299/224362935-82399623-60f3-4fc1-bf78-5d4bc1ca33bd.png)

Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(solver_example)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib ${CMAKE_CURRENT_BINARY_DIR}/solver_lib)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter_ex)

add_executable(example equation.cpp)

target_link_libraries(example solver_lib formatter_ex)
```

- Команды аналогичны заданию 2 и 3

```
$ git add CMakeLists.txt
$ git commit -m "added CMakeLists.txt"
$ git push origin lab
$ git add equation.cpp
$ git commit -m "added equation.cpp"
$ git push origin lab
```

Проверяем работоспособность CMake:
```
$ cmake -H. -B_build
$ cmake --build _build
```
![Снимок экрана от 2023-03-05 23-16-39](https://user-images.githubusercontent.com/125737299/224363042-688fdec4-68bf-4499-bd16-f1833186bba0.png)


Демонстрируем исполнение программы:
```
$ cmake --build _build --target example
$ ./_build/example
```

### hello_world.cpp

```
$ git checkout -b lab
$ cat >> CMakeLists.txt << EOF
> EOF
$ nano CMakeLists.txt
```
![Снимок экрана от 2023-03-05 23-21-17](https://user-images.githubusercontent.com/125737299/224363082-e16e1ece-58b0-4c46-bb1b-c1946fa58a0b.png)

Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(hello_world_example)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter_ex)
add_executable(example hello_world.cpp)

target_link_libraries(example formatter_ex)
```

- Команды аналогичны заданию 2 и 3

```
$ git add CMakeLists.txt
$ git commit -m "added CMakeLists.txt"
$ git push origin lab
$ git add hello_world.cpp
$ git commit -m "added hello_world.cpp"
$ git push origin lab
```

Проверяем работоспособность CMake:
```
$ cmake -H. -B_build
$ cmake --build _build
```
![Снимок экрана от 2023-03-05 23-21-30](https://user-images.githubusercontent.com/125737299/224363101-1614ecfb-4b8d-4ba9-a238-d3c3320c4ad9.png)


Демонстрируем исполнение программы:
```
$ cmake --build _build --target example
$ ./_build/example
```
![Снимок экрана от 2023-03-05 23-35-17](https://user-images.githubusercontent.com/125737299/224363143-e47d63a6-3cdf-4305-a72f-4a26114886e1.png)


## Required libraries
```
$ sudo apt install cmake - устанавливаем пакет cmake
```
