# Cmake
Na podstawie: https://cmake.org/cmake/help/latest/guide/tutorial/index.html
## Podstawy
Mamy tu minimalny przykład
```cmake
#na początku zawsze określamy min wersję CMake'a
cmake_minimum_required(VERSION 3.10)

# set the project name
project(Tutorial)

# Tworzymy tylko jeden plik wyjściowy `Tutorial` ze skompilowanego pliku tutorial.cxx
add_executable(Tutorial tutorial.cxx)
```

## Budowanie
```bash
#warto stworzyć sobie nowy folder i w nim budować
mkdir build; cd build

cmake SCIEZKA_DO_FOLDERU_GLOWNEGO # zwykle do folderu z plikiem CMakeLists.txt
cmake --build #można tu też użyć po prostu make (Linux)

```


## Konfigurowalne pliki nagłówkowe
Za pomocą CMake'a możemy generować pliki nagłówkowe zawierające zmienne oraz parametry zawarte w plikach CMake. 

Przykładowo możemy w ten sposób zapisywać wersję naszego programu.
```cmake
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(Tutorial VERSION 1.0)

# opisujemy tu na podstawie czego ma być wygenerowany nasz plik nagłówkowy
configure_file(TutorialConfig.h.in TutorialConfig.h)

# Skoro utworzony zostanie plik TutorialConfig.h to warto dodać ścieżkę na krórej się znajduje do listy ścieżek w których będą szukane pliki
target_include_directories(Tutorial PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           )

```
Zawartość pliku TutorialConfig.h.in
```cpp
// the configured options and settings for Tutorial
#define Tutorial_VERSION_MAJOR @Tutorial_VERSION_MAJOR@
#define Tutorial_VERSION_MINOR @Tutorial_VERSION_MINOR@

```

## Określenie wymaganej wersji C++

```cmake
# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
```

## Biblioteki

### Tworzenie własnych
Podobnie jak programy, za pomocą cmake'a możemy definiować też biblioteki
W wypadku prostych bibliotek wewnątrz naszych preojektów wystarczy jednolinijkowy plik `CMakeLists.txt` w ich folderze.
```cmake
# Dodaj bibliotekę o nazwie MathFunctions zawierającą plik mysqrt.cxx
add_library(MathFunctions mysqrt.cxx)
```
(Ta biblioteka znajduje się w folderze `MathFunctions` w głównym folderze projektu. W folderze tym mamy jeszcze plik nagłówkowy `MathFunctions.h`)
### Linkowanie bibliotek

```cmake
# add the MathFunctions library
add_subdirectory(MathFunctions)

# add the executable
add_executable(Tutorial tutorial.cxx)

# Musimy podlinkować wszystkie biblioteki używane przez plik Tutorial
target_link_libraries(Tutorial PUBLIC MathFunctions)

# add the binary tree to the search path for include files
# so that we will find TutorialConfig.h
target_include_directories(Tutorial PUBLIC
                          "${PROJECT_BINARY_DIR}"
                          "${PROJECT_SOURCE_DIR}/MathFunctions"
                          )
```

## Logika

### Zmienne

### Opcje

### IF-y


## Domyślne ścieżki w CMake

TODO




```cmake

```