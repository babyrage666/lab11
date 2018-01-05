[![Build Status](https://travis-ci.org/babyrage666/lab11.svg?branch=master)](https://travis-ci.org/babyrage666/lab11)
## Laboratory work XI

Данная лабораторная работа посвещена изучению компонентов **Boost** на примере `program_options`

```ShellSession
$ open http://www.boost.org/doc/libs/1_65_0/doc/html/program_options.html
```

## Tasks

- [X] 1. Создать публичный репозиторий с названием **lab11** на сервисе **GitHub**
- [X] 2. Выполнить инструкцию учебного материала
- [X] 3. Ознакомиться со ссылками учебного материала
- [X] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial
Определяем глобальные переменные.
```ShellSession
$ export GITHUB_USERNAME=babyrage666
$ alias edit=subl
$ alias gsed=sed # for *-nix system
```
Подготовка к выполнению **Лабораторной работы №11**.
Проводим первоначальные настройки для соединения с репозиторием 11 лабораторной работы
```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab10 lab11
$ cd lab11
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab11
```
Подключаем пакеты **boost::program_options** через **hunter** и редактируем **demo.cpp**, используя пакет **boost::program_options** для выполнения дальнейших команд
```ShellSession
# boost::program_options
# Редактируем CMakeLists.txt
$ edit CMakeLists.txt
# Редактируем sources/demo.cpp
$ edit sources/demo.cpp
```

Собираем проект с **CMake**.
```ShellSession
# -H. устанавливаем каталог в который сгенерируется файл CMakeLists.txt
# -B_build указывает директорию для собираемых файлов
# -D - заменяет команду set
$ cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
# --build _build создает бинарное дерево проекта
# --target указывает необходимые для обработки цели
$ cmake --build _build --target install
# Создаем директорию artifacts меняем директорию на artifacts
$ mkdir artifacts && cd artifacts
```
Создаем **default.log**.
```ShellSession
# C помощью нашей программы записываем "text1 text2 text3" в default.log
$ echo "text1 text2 text3" | ../_install/bin/demo
# Проверяем наличие данного файла
$ test -f default.log
# Если 0, то файл существует, что соответствует истине
$ echo $?
0
```
Создаем **config.log**.
```ShellSession
# Создаем директорию ${HOME}/.config
$ mkdir ${HOME}/.config
# Вводим в demo.cfg значение output=config.log для дальнейшего вывода
$ echo "output=config.log" > ${HOME}/.config/demo.cfg
# C помощью нашей программы записываем "text1 text2 text3" в config.log
$ echo "text1 text2 text3" | ../_install/bin/demo
# Проверяем наличие данного файла
$ test -f config.log
# Если 0, то файл существует, что соответствует истине
$ echo $?
0
```
Создаем **env.log**.
```ShellSession
# Экспортируем глобальную переменную окружения DEMO_OUTPUT
$ export DEMO_OUTPUT=env.log
# C помощью нашей программы записываем "text1 text2 text3" в env.log
$ echo "text1 text2 text3" | ../_install/bin/demo
# Проверяем наличие данного файла
$ test -f env.log
# Если 0, то файл существует, что соответствует истине
$ echo $?
0
```
Создаем **arg.log**.
```ShellSession
# C помощью нашей программы записываем "text1 text2 text3" в arg.log, задавая его с помощью --output
$ echo "text1 text2 text3" | ../_install/bin/demo --output arg.log
# Проверяем наличие данного файла
$ test -f arg.log
# Если 0, то файл существует, что соответствует истине
$ echo $?
0
```
Редактируем **README.md**.
```ShellSession
gsed -i 's/lab10/lab11/g' README.md
```
Редактируем **.travis.yml**.
```ShellSession
$ cat >> .travis.yml <<EOF
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build --target install
- mkdir artifacts && cd artifacts
- echo "text1 text2 text3" | ../_install/bin/demo
- test -f default.log
- mkdir ${HOME}/.config
- echo "output=config.log" > ${HOME}/.config/demo.cfg
- echo "text1 text2 text3" | ../_install/bin/demo
- test -f config.log
- export DEMO_OUTPUT=env.log
- echo "text1 text2 text3" | ../_install/bin/demo
- test -f env.log
- echo "text1 text2 text3" | ../_install/bin/demo --output arg.log
- test -f arg.log
EOF
```
Отправка данных на удаленный репозиторий **GitHub**.
```ShellSession
$ git add .
$ git commit -m"changed format output"
$ git push origin master
```
Подключаем **TravisCI**.
```ShellSession
$ travis login --auto
$ travis enable
```

## Report

```ShellSession
$ popd
$ export LAB_NUMBER=11
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [String Algorithms](http://www.boost.org/doc/libs/1_65_0/doc/html/string_algo.html)
- [Date Time](http://www.boost.org/doc/libs/1_65_0/doc/html/date_time.html)
- [DLL](http://www.boost.org/doc/libs/1_65_0/doc/html/boost_dll.html)
- [Heap](http://www.boost.org/doc/libs/1_65_0/doc/html/heap.html)
- [Interprocess](http://www.boost.org/doc/libs/1_65_0/doc/html/interprocess.html)
- [Lockfree](http://www.boost.org/doc/libs/1_65_0/doc/html/lockfree.html)
- [Lexicalcast](http://www.boost.org/doc/libs/1_65_0/doc/html/boost_lexical_cast.html)
- [Property Tree](http://www.boost.org/doc/libs/1_65_0/doc/html/property_tree.html)

```
Copyright (c) 2017 Братья Вершинины
```
