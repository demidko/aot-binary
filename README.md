# aot-compiler

Компилятор aot-словаря русской морфологии в собственный бинарный формат, оптимизированный загрузки в память и быстрого поиска.  

## Оригинальный текстовый формат

За основу для оптимизации был взят [проект aot](https://github.com/sokirko74/aot). На вход нашему компилятору подаются оригинальные [aot-словари морфологии русского языка](https://github.com/sokirko74/aot/tree/master/Dicts/Morph/Russian). Они хорошо задокументированы [здесь](https://github.com/sokirko74/aot/blob/master/Docs/Morph_UNIX.txt).

## Оптимизированный бинарный формат

```
количество морфологий
морфология
...
морфология 

количество строк
строка
...
строка

количество лемм
(индекс строки, индекс морфологии) (индекс строки, индекс морфологии)... (индекс строки, индекс морфологии) (индекс строки, индекс морфологии)
(индекс строки, индекс морфологии) (индекс строки, индекс морфологии)... (индекс строки, индекс морфологии) (индекс строки, индекс морфологии)
...
(индекс строки, индекс морфологии) (индекс строки, индекс морфологии)... (индекс строки, индекс морфологии) (индекс строки, индекс морфологии)

количество хешей (коллизии проверяются в рантайме, нет смысла отделяеть их во время компиляции, т. к. могут быть и внешние коллизии)
хеш, индекс леммы, индекс леммы
хеш, индекс леммы, индекс леммы, индекс леммы
хеш, индекс леммы, индекс леммы, индекс леммы, индекс леммы
...
хеш, индекс леммы, индекс леммы, индекс леммы
```

## Build with Java

Execute `./gradlew clean build`. Your jar will be located at `./build/libs` with `-all.jar` postfix.
Now you can run:

```shell
java -jar aot-compiler-all.jar
```

## Or, build with Docker

Execute `docker build . -t aot-compiler`. Your image will be located at `docker images -a`. Now you can
run:

```shell
docker run -it --rm aot-compiler
```
