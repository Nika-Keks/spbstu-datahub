# spbstu-datahub

Репозиторий для доступа и версионирования данных


## Структура 
---

### Ветвления

Каждая ветка представляет из себя один датасет кроме веток:

+ base - базовая ветка для всех датасетов
+ instruction - ветка с инструкцией

Для создания нового датасета нужно ответвиться от base и добавить файлы 
+ data.dvc - файл с ивформацией о находдении данных
+ models/\<model-name> - сохраненная модель (.pth, .h5)


`ВНИМАНИЕ: необходимо соблюдать структуру файлов!`

---
### Структура файлов    

    .
    |-- models # директория с предобученными моделями
    |   |-- model-1.h5.dvc
    |   |-- model-2.h5.dvc
    |   |-- ...
    |   |-- README.md # описания моделей и зависимостей
    |-- data.dvc # директория с данными
    |-- README.md # описание структуры данных 

## Управление
---
Управление данными и моделями осуществляется с помощью [dvc](https://dvc.org/doc). Все файлы хранятся в S3 хранилище, для доступа необходимы ключи, для их ввода можно использовать модуль [spbstu-amml](https://github.com/Nika-Keks/spbstu-amml.git)

### Пример использования
---
Добавление данных
```console
$ git checkout base             # переходим в ветку base
$ git checkout -b ${my_dataset} # создаем ветку датасета (от base!)
$ dvc abb data                  # добавление данных
$ git add data.dvc .gitignore   # .gitignore, чтобы данные не попали в репозиторий
$ git commit -m "added data"    # 
$ dvc push data.dvc             # отправляем данные в хранилище
```
Аналогично для моделей
```console
$ git checkout base 
$ git checkout ${my_dataset}
$ dvc add models/${model_name}
$ git add models/${model_name} models/.gitignore
...
```