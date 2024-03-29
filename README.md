## Урок 8. Скрипты Bash
# Задание

#### 1. Написать скрипт очистки директорий.
На вход принимает путь к директории.
Если директория существует, то удаляет в ней все файлы с расширениями .bak, .tmp, .backup.
Если директории нет, то выводит ошибку.

# Выполнение:
a. Создаем и открываем файл следующей командой (можно так же открыть в редакторе nano командой "nano delfiletodir"):

```  cat > delfiletodir ```

b. Далее прописываем текст, указанный ниже:

```   #!/bin/bash

read -p "Введите путь к дирректории: " DELDIR

if [ -e $DELDIR ]
    then
        echo 'Указанная дирректория найдена'
        cd $DELDIR
        echo 'Произвожу удаление'
        rm -v *.bak *.tmp *.backup
        echo 'Удаление завершено успешно'
    else
        echo 'Указанная дирректория не найдена! Выполнение остановлено'
        exit 2
fi

```

c. Сохраняем и запускаем в Bash:

``` bash delfiletodir ```

#### 2. Создать скрипт ownersort.sh, который в заданной папке копирует файлы в директории, названные по имени владельца каждого файла.
Учтите, что файл должен принадлежать соответствующему владельцу.
#Выполнение

a. Сначала считываем всех владельцев файлов в директории, убираем повторения и делаем папки по одной для каждого:
```
#!/bin/bash

dir=$(ls -l | tr -s ' ' '\t' | cut -f '3' | sort -u)
for i in $dir; do
    mkdir -p $i
done
```
b. Теперь считываем владельцев и названия. Проходимся по ним циклом (нечётное - владелец, чётное - название) Если название - проверяем, что это файл, а не папка. Если файл - отправляем в директорию с именем хозяина:
```
dirfile=$(ls -l | tr -s ' ' '\t' | cut -f '3 9')
count=0
for i in $dirfile; do
    count=$((count+1))
        if (($count%2))
            then
                dir=$i
                echo $dir = $i zero
            else
                if [ -f ./$i ]
                    then
                        cp ./$i ./$dir/$i
                fi
        fi
done
```
# Результат
Код скриптов в текстовом виде (каждый скрипт в отдельном файле). Кодировка файлов UTF-8.
