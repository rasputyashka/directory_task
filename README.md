OOP \ Рекурсия \ AoC

# Условие
У вас есть устройство с терминалом и файловой системой, терминал поддерживает две команды: ls и cd. Каждая папка имеет свой размер равный сумме размеров всех объектов в ней.

все команды начинаются с `$ `

команда ls отображает **только текущую** директорию

информация, которую может выдать команда ls:

```bash
$ ls
dir some_directory
12341234 filename.txt
```
`some_directory` является директорией
`filename.txt` является файлом размером **12341234**

команда cd меняет текущую директорию на:

* родителя в случае `$ cd ..`
* указанную папку, находящуюся в текущей директории в случае `$ cd dirname`
* на папку корня в случае с `$ cd /`


## Что делать
1) Вам дана последовательность команд и их выхлопов, вам нужно создать класс `Directory` и класс `FileObject` и заполнить корневую папку данными, полученными из ввода. Создать дерево файловой системы (дерево папок). В каждой папке могут находиться файлы и другие папки. **Этот пункт проверяется код ревьюером (которого вы, надеюсь, найдёте в чате), не тестирующей системой**

2) Выведите сумму всех папкок, размер которых не превышает 100000.

Пример: 

**Вход**: 
```bash
$ cd /
$ ls
dir a
14848514 b.txt
8504156 c.dat
dir d
$ cd a
$ ls
dir e
29116 f
2557 g
62596 h.lst
$ cd e
$ ls
584 i
$ cd ..
$ cd ..
$ cd d
$ ls
4060174 j
8033020 d.log
5626152 d.ext
7214296 k
```

**Вывод**:
```95437```

(пояснение к примеру): 
структура вашей файловой системы выглядит так:
```
- / (dir)
  - a (dir)
    - e (dir)
      - i (file, size=584)
    - f (file, size=29116)
    - g (file, size=2557)
    - h.lst (file, size=62596)
  - b.txt (file, size=14848514)
  - c.dat (file, size=8504156)
  - d (dir)
    - j (file, size=4060174)
    - d.log (file, size=8033020)
    - d.ext (file, size=5626152)
    - k (file, size=7214296)
```
размер папки `e` равен **584**

размер папки `a` равен **94853** (она содержит в себе ещё и папку `e`)

рамзер папки `d` равен **24933642**

размер папки `/` равен **48381165** (она содержит в себе все папки выше)

PS: Структуру проекта я стырил со своей утилиты [jjm](https://github.com/rasputyashka/jjm), которую я писал для себя, но вы можете её форкнуть при необходимости
