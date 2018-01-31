## Лабораторная работа №4. Отчет.

## Задание на лабораторную работу:

1. Создать публичный репозиторий с названием lab04 на сервисе GitHub
2. Ознакомиться со ссылками учебного материала
3. Выполнить инструкцию учебного материала
4. Составить отчет и отправить ссылку личным сообщением в Slack

## Выполнение работы.
	
В соответствии с последовательностью, определенной заданием на лабораторную работу, были выполнены следующие действия:
1. Создан новый пустой репозиторий https://github.com/vaulex/lab04 с лицензией MIT, попутно создан файл .gitignore следующего содержания:
```ShellSession
*build*/
*install*/
*.swp
.idea/
```
2. Проведено ознакомление по приведенным ссылкам со следующими материалами https://cmake.org/, Autotools.
3. Выполнена следующая последовательность команд:

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=vaulex
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
$ source scripts/activate
$ git clone https://github.com/${GITHUB_USERNAME}/lab03.git projects/lab04
$ cd projects/lab04
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab04.git
$ g++ -I./include -std=c++11 -c sources/print.cpp
$ ls print.o
$ nm print.o | grep print
$ ar rvs print.a print.o
$ file print.a
$ g++ -I./include -std=c++11 -c examples/example1.cpp
$ ls example1.o
$ g++ example1.o print.a -o example1
$ ./example1 && echo
$ g++ -I./include -std=c++11 -c examples/example2.cpp
$ nm example2.o
$ g++ example2.o print.a -o example2
$ ./example2
$ cat log.txt && echo
$ rm -rf example1.o example2.o print.o 
$ rm -rf print.a 
$ rm -rf example1 example2
$ rm -rf log.txt
$ cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.0)
project(print)
EOF
$ cat >> CMakeLists.txt <<EOF
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
EOF
$ cat >> CMakeLists.txt <<EOF
add_library(print STATIC \${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
EOF
$ cat >> CMakeLists.txt <<EOF
include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/include)
EOF
$ cmake -H. -B_build
$ cmake --build _build
$ cat >> CMakeLists.txt <<EOF

add_executable(example1 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
add_executable(example2 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
EOF
$ cat >> CMakeLists.txt <<EOF

target_link_libraries(example1 print)
target_link_libraries(example2 print)
EOF
$ cmake --build _build
$ cmake --build _build --target print
$ cmake --build _build --target example1
$ cmake --build _build --target example2
$ ls -la _build/libprint.a
$ _build/example1 && echo
hello
$ _build/example2
$ cat log.txt && echo
hello
$ rm -rf log.txt
$ git clone https://github.com/tp-labs/lab04 tmp
$ mv -f tmp/CMakeLists.txt .
$ rm -rf tmp
$ cat CMakeLists.txt
$ cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
$ cmake --build _build --target install
$ tree _install
$ git add CMakeLists.txt
$ git commit -m"added CMakeLists.txt"
$ git push origin master
```

## Report
```ShellSession
$ popd
$ export LAB_NUMBER=04
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```


## В результате выполнения блока Tutorial и Report:
	
осуществлена компиляция с помощью средств g++ и запуск программ print.cpp, example1.cpp, example2.cpp;
выполнена настройка конфигурационного файла cmake;
осуществлена компиляция с помощью пакета cmake и запуск программ print.cpp, example1.cpp, example2.cpp с помощью средств g++;
в обоих случаях результат выполнения программы example2.cpp (фраза «hello») записывался в файл log.txt;
осуществлено наполнение репозитория lab04 файлами, содержащими CmakeLists.txt и отчетом.

Составлен отчет о работе.

	
## Выводы
В ходе проделанной работы проведена ознакомительная работа с работой компилятора g++ и средства автоматизации сборки cmake.
