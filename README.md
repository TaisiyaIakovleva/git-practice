# git-practice

# Лабораторная работа 1

## Задание
Модифицировать файл `script.bash` так, чтобы при его запуске в терминале в виде

```bash
bash script.bash Vasya Pupkin
```

Вывод был

`Welcome, Vasya Pupkin`

## Ход выполнения работы

Создала новый файл с именем `script.bash` с помощью команды:

```bash
touch script.bash
```
Открыла файл для редактирования:

![Описание изображения](/images/lab1.png)

`$*` объединяет все переданные скрипту аргументы в одну строку, разделённую пробелами

Итоговый вывод:

![Описание изображения](/images/lab1-result.png)

# Лабораторная работа 2

## Задание
1. Создать скрипт для выполнения арифметических операций с двумя аргументами (сумма, разность, произведение).
2. Реализовать скрипт, который преобразует IPv4-адрес из десятичного в двоичный формат.

## Ход выполнения работы

#### Арифметические операции с двумя элементами
Создала новый файл с именем `script.bash` с помощью команды:

```bash
touch script.bash
```
Открыла файл для редактирования:

![Описание изображения](/images/lab2.png)

Итоговый вывод:

![Описание изображения](/images/lab2-res.png)

#### Преобразование IPv4-адрес из десятичного в двоичный форма


Изменила файл`script.bash`:


![Описание изображения](/images/lab2-ip.png)

Аргумент, переданный скрипту, записывается в переменную `ip`
`IFS='.'` задаёт разделителем точку
Команда bc переводит число a в двоичную систему (`obase=2`)


Итоговый вывод:

![Описание изображения](/images/lab2-res-ip.png)


# Лабораторная работа 3

## Задание
Необходимо настроить виртуальную машину А с Ubuntu в VirtualBox. Обеспечить доступ в сеть Интернет. Осуществить проверку этого доступа и приложить скриншот из терминала. Следующим шагом настроить ещё одну виртуальную машину Б. После чего обеспечить сетевой доступ от машины А к машину Б. Приложить скриншот из терминала. Поднять ещё одну виртуальную машину В. Организовать сетевой доступ:

1. из машины А в машину Б.
2. из машины А в машину В,
3. но запретить доступ из машины Б в машину В.

Приложить скриншот, на котором видно терминалы всех трёх машин.

## Ход выполнения работы

#### Настройка виртуальной машины А (VMA)

Подключили машину А к сети `NAT` для доступа в Интернет

![Описание изображения](/images/A-сеть.jpg)

Настроила статический IP-адрес для машины А

![Описание изображения](/images/vmA-ip.jpg)

Итоговый вывод:
![Описание изображения](/images/pingA-google.jpg)

ping прошел успешно
#### Настройка виртуальной машины Б (VMB)

Подключила машину В к сети intnet
![Описание изображения](/images/vmB-adap.jpg)

Добавила машину А во внутреннюю сеть intnet через второй адаптер
![Описание изображения](/images/vmA-adap2.jpg)

Настроила статический IP-адрес для машины B

![Описание изображения](/images/vmB-ip.jpg)

Итоговый вывод:
![Описание изображения](/images/pingAB-BA.jpg)

ping прошел успешно
#### Настройка виртуальной машины В (VMC)

Подключила машину C к сети intnet
![Описание изображения](/images/vmC-adap.jpg)

Настроила статический IP-адрес для машины C
![Описание изображения](/images/vmC-ip.jpg)

Настроили iptables на машине C для блокировки трафика с машины B

Итоговый вывод:

![Описание изображения](/images/lab3-result.JPG)

Доступ из машины A в машину C успешно настроен, а из машины B в машину C запрещен


# Лабораторная работа 4

## Задание
Запустить в контейнере приложение “aafire”. Настроить сеть между двумя контейнерами.


## Ход выполнения работы

Создала файл `Dockerfile` со следующим содержимым:

![Описание изображения](/images/Dockerfile.jpg)

- FROM ubuntu:latest — базовый образ Ubuntu
- RUN — обновление пакетов и установка aafire и ping

Собрала Docker-образ с помощью команды:

```bash
docker build -t aafire_image
```

Запустила контейнер с приложением `aafire`

```bash
docker run -itd --name aafire_container1 aafire_image /usr/bin/aafire
```
![Описание изображения](/images/fire.jpg)

Запустила второй контейнер 

```bash
docker run -itd --name aafire_container2 aafire_image
```

Создала сеть для взаимодействия контейнеров:

```bash
docker network create myNetwork
```

Подключила оба контейнера к сети

```bash
docker network connect myNetwork aafire_container1
docker network connect myNetwork aafire_container2
```

Получаю IP-адрес второго контейнера
![Описание изображения](/images/lab4-ip.jpg)

Выполняю тест связи из первого контейнера:
![Описание изображения](/images/lab4-ping.jpg)

ping прошел успешно

# Лабораторная работа 5

## Ход выполнения работы

#### Введение

Создала репозиторий git-practice на Github, скопировала URL репозитория

Клонирую репозиторий:
```bash
git clone https://github.com/TaisiyaIakovleva/git-practice
cd git-lab
```
Добавляю файл

```bash
MacBook-Pro-2:git-practice Taisia1$ touch example.txt 
MacBook-Pro-2:git-practice Taisia1$ vim example.txt 
MacBook-Pro-2:git-practice Taisia1$ git add example.txt
MacBook-Pro-2:git-practice Taisia1$ git commit -m "File added example.txt"
MacBook-Pro-2:git-practice Taisia1$ git push origin main
```
Создаю ветку и переключаюсь на нее

```bash
MacBook-Pro-2:git-practice Taisia1$ git branch feature-branch
MacBook-Pro-2:git-practice Taisia1$ git checkout feature-branch
```

Редактирую файл example.txt

```txt
Книга

Предисловие
Глава 1
Глава 2
Глава 3
Глава 4
```

Переключаюсь в основную ветку

```bash
MacBook-Pro-2:git-practice Taisia1$ git checkout main
```

Сливаю изменения из ветки feature-branch в основную ветку:

```bash
MacBook-Pro-2:git-practice Taisia1$ git merge feature-branch
MacBook-Pro-2:git-practice Taisia1$ git push origin main
```

#### Работа с ветками
Создала новый текстовый файл book.txt с базовой структурой книги:

```txt
# Название книги

## Глава 1: Введение
Здесь будет введение в тему книги.

## Глава 2: Основы Git
Основные понятия и команды Git.
```

Создала ветку "feature-login" для разработки новой функциональности:
```bash
MacBook-Pro-2:git-practice Taisia1$ git checkout feature-login
```

Внесла изменения в файл:

```txt
# Название книги

## Глава 1: Введение
Здесь будет введение в тему книги.

## Глава 2: Основы Git
Основные понятия и команды Git.

## Глава 3: Вход в систему
Раздел по новой функциональности входа в систему.
```

Завершила изменения, закоммитила их и отправила ветку на GitHub:

```bash
MacBook-Pro-2:git-practice Taisia1$ git add book.txt
MacBook-Pro-2:git-practice Taisia1$ git commit -m "Добавлена глава 3: Вход в систему"
MacBook-Pro-2:git-practice Taisia1$ git push origin feature-login
```

#### Работа с удаленным репозиторием

Переключилась на основную ветку (main) и внесите изменения:
```bash
MacBook-Pro-2:git-practice Taisia1$ git checkout main
```
Внесла изменения в основной ветке (добавила описание книги):

```txt
# Название книги: Приключения в мире Git

## Глава 1: Введение
Здесь будет введение в удивительный мир Git.

## Глава 2: Основы Git
Основные понятия и команды Git.
```

Закоммитьтила изменения и отправила их на GitHub:

```bash
MacBook-Pro-2:git-practice Taisia1$ git add book.txt
MacBook-Pro-2:git-practice Taisia1$ git commit -m "Изменено название книги и введение"
MacBook-Pro-2:git-practice Taisia1$ git push origin main
```

#### Моделирование конфликта

Вернулась в ветку "feature-login" и внесла изменения в том же участке:

```bash
MacBook-Pro-2:git-practice Taisia1$ git checkout feature-login
```

Изменила главу 2 в файле

```txt
# Название книги: Приключения в мире Git

## Глава 1: Введение
Здесь будет введение в удивительный мир Git.

## Глава 2: Основы Git и магия конфликтов
Основные понятия и команды Git, а также волшебство разрешения конфликтов.
```
Закоммитьтила изменения и отправила их на GitHub:

```bash
MacBook-Pro-2:git-practice Taisia1$ git add book.txt
MacBook-Pro-2:git-practice Taisia1$ git commit -m "Добавлен раздел о магии конфликтов"
MacBook-Pro-2:git-practice Taisia1$ git push origin feature-login
```

#### Разрешение конфликта

Вернулась в основную ветку и попробовала слить изменения:
```bash
MacBook-Pro-2:git-practice Taisia1$ git checkout main
MacBook-Pro-2:git-practice Taisia1$ git pull origin main
```

Возник конфликт. Разрешаем его в файле

```txt
# Название книги: Приключения в мире Git

## Глава 1: Введение
Здесь будет введение в удивительный мир Git.

<<<<<<< HEAD
## Глава 2: Основы Git и магия конфликтов
Основные понятия и команды Git, а также волшебство разрешения конфликтов.
======= 
## Глава 2: Основы Git
Основные понятия и команды Git. 
>>>>>>> feature-login
```


Разрешаю конфликт, удалив метки и оставив нужные изменения:

```txt
# Название книги: Приключения в мире Git

## Глава 1: Введение
Здесь будет введение в удивительный мир Git.

## Глава 2: Основы Git и магия конфликтов
Основные понятия и команды Git, а также волшебство разрешения конфликтов.
```


Закоммитьтила разрешение конфликта и отправила изменения на GitHub:

```bash
MacBook-Pro-2:git-practice Taisia1$ git add book.txt
MacBook-Pro-2:git-practice Taisia1$ git commit -m "Resolved conflict in chapter 2"
MacBook-Pro-2:git-practice Taisia1$ git push origin main
```

#### Автоматизация проверки формата файлов при коммите

Создала скрипт `check_format.sh`

![Описание изображения](/images/lab5sh.png)

Проверила, что формат проверяется автоматически

![Описание изображения](/images/lab5-format.png)


#### Использование Git Flow в проекте

Выполнила команду и следовала инструкциям:

![Описание изображения](/images/lab5-1.png)
![Описание изображения](/images/lab5-2.png)

Создала ветку для новой функциональности:
```bash
MacBook-Pro-2:git-practice Taisia1$ git flow feature start task-management
```

Добавила код в файл `task_manager.py`:
```python
def create_task(title, description):
    # Логика создания задачи
    print(f"Создана новая задача: {title}")
```

Закоммитила изменения:
```bash
MacBook-Pro-2:git-practice Taisia1$ git add task_manager.py
MacBook-Pro-2:git-practice Taisia1$ git commit -m "Добавлен функционал управления задачами"
```

Завершила работу с веткой:
```bash
MacBook-Pro-2:git-practice Taisia1$ git flow feature finish task-management
```
Переключилась на ветку `develop` и начала релиз:
```bash
MacBook-Pro-2:git-practice Taisia1$ git checkout develop
MacBook-Pro-2:git-practice Taisia1$ git flow release start v1.0.0
```
Обновила файл версии:
```bash
MacBook-Pro-2:git-practice Taisia1$ echo "v1.0.0" > version.txt
MacBook-Pro-2:git-practice Taisia1$ git add version.txt
MacBook-Pro-2:git-practice Taisia1$ git commit -m "Обновлена версия для релиза v1.0.0"
```
Завершила релиз:

![Описание изображения](/images/lab5-3.png)

