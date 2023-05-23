# lab03

**Task 1**
С помощью `brew install cmake` скачиваю все необходимые инструменты
```
mkdir formatter_lib
cd formatter_lib
wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_lib/formatter.h
wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_lib/formatter.cpp
nano CMakeLists.txt

cmake_minimum_required(VERSION 3.4)
project(formatter_lib)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_library(formatter_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/formatter.cpp)
```
Проверяю, что проект собирается `cmake -B build`, `cmake --build build`

![0DC6A312-3C6C-4405-9E8B-1719CCFABED5_4_5005_c](https://github.com/nastyanam05/lab03/assets/112873954/a0face30-e989-437f-81fe-271f604e1f97)

![C2FC32F0-414B-48F0-95FA-DD5D67509B98_4_5005_c](https://github.com/nastyanam05/lab03/assets/112873954/2ed3a3e1-53d5-4b3f-a430-74d1e1317908)

**Task 2**
```
mkdir formatter_ex_lib
cd formatter_ex_lib
wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_ex_lib/formatter_ex.cpp
wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_ex_lib/formatter_ex.h
nano CMakeLists.txt

cmake_minimum_required(VERSION 3.4)
project(formatter_ex_lib)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib formatter_lib_dir)
add_library(formatter_ex_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex.cpp)
target_include_directories(formatter_ex_lib PUBLIC
${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib
)
target_link_libraries(formatter_ex_lib formatter_lib)
```
Проверяю, что проект собирается `cmake -B build`, `cmake --build build`

![364E7838-0C97-4504-A5DA-123467EA1C82_1_201_a](https://github.com/nastyanam05/lab03/assets/112873954/7bfb3f9d-c8ff-4d4b-9bf0-19d2d998a135)

![33C697D8-A9AF-4BA6-B4CE-BE4EF239D2E1_1_201_a](https://github.com/nastyanam05/lab03/assets/112873954/caf3317a-de4f-406c-aeca-1e5207a5d504)

**Task 3**
```
mkdir hello_world_application
cd hello_world_application
wget https://raw.githubusercontent.com/tp-labs/lab03/master/hello_world_application/hello_world.cpp
nano CMakeLists.txt

cmake_minimum_required(VERSION 3.4)
project(hello_world)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib formatter_ex_lib_dir)
add_executable(hello_world ${CMAKE_CURRENT_SOURCE_DIR}/hello_world.cpp)
target_include_directories(hello_world PUBLIC
${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib
)
target_link_libraries(hello_world formatter_ex_lib)
```
Проверяю, что проект собирается `cmake -B build`, `cmake --build build`

![A83F5EE4-9278-4589-A754-8EB9D64C7CBA_1_201_a](https://github.com/nastyanam05/lab03/assets/112873954/092516ff-3b31-4305-adad-85cbf408b0af)

![B3E8C547-02B5-452D-80A4-0DE99E871CA0_1_201_a](https://github.com/nastyanam05/lab03/assets/112873954/71a470c5-2954-42e7-ac5b-0fbc2f7d0f36)

Проверяю работу `build/hello_world`

![0DF25F03-8CCA-4525-B8A1-2AC8DF2BB917_4_5005_c](https://github.com/nastyanam05/lab03/assets/112873954/63f3a8c2-1fd8-45a1-959d-10ab4680a99f)

Cоберу библиотеку solver_lib.
В коде библиотеки есть ошибка: не хватает библиотеки cmath, а sqrtf не лежит в std. Исправляю это.
Директория solver_lib, файл CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)
project(solver_lib)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_library(solver_lib ${CMAKE_CURRENT_SOURCE_DIR}/solver.cpp)
```
Директория solver_application, файл CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)
project(solver)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib formatter_ex_lib_dir)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib solver_lib_dir)
add_executable(solver ${CMAKE_CURRENT_SOURCE_DIR}/equation.cpp)
target_include_directories(formatter_ex_lib PUBLIC
${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib
${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib
)
target_link_libraries(solver formatter_ex_lib solver_lib)
```
Проверяю `cmake -B build`, `cmake --build build` и `build/solver`

![78769371-1174-4049-85CC-7E7A43758931_1_201_a](https://github.com/nastyanam05/lab03/assets/112873954/d920792b-6ea2-4d38-92d0-253ee1a9b7c5)

![5AB5B0F2-7155-417D-A6F0-B26F9B42C18E_1_201_a](https://github.com/nastyanam05/lab03/assets/112873954/b58618a0-9d7e-4470-9fdb-b68dd34902f5)

Все работает!
