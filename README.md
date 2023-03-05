# Report-01

## 1. Скачайте библиотеку boost с помощью утилиты `wget`
 
```
$ wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
```

## 2. Разархивируйте скаченный файл в директорию `~/boost_1_69_0` 

```
$ tar -xvf boost_1_69_0.tar.gz
```

![4zLVsrrjzfY](https://user-images.githubusercontent.com/125737299/222975793-885dbb42-2f2e-4887-8c56-e3fc5efddcdb.jpg)

## 3. Подсчитайте количество файлов в директории `~/boost_1_69_0` не включая вложенные директории

```
$ ls -l | grep "^-" | wc -l
```
![Снимок экрана от 2023-02-28 20-38-49](https://user-images.githubusercontent.com/125737299/221937919-dcef5da0-15f1-4f0c-be08-1a4ab09f1609.png)

## 4. Подсчитайте количество файлов в директории `~/boost_1_69_0` включая вложенные директории

```
$ ls -l -R | wc -l
```
![Снимок экрана от 2023-02-28 20-39-23](https://user-images.githubusercontent.com/125737299/221938142-1d358652-4884-4775-a8c7-c886acf0bbd4.png)

## 5. Подсчитайте количество заголовочных файлов, файлов с расширением `.cpp`, сколько остальных файлов (не заголовочных и не `.cpp`)
