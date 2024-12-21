# Лабораторная работа 5

## Задание 1 - Автоматизация проверки формата файлов при коммите

1. Я создал файл pre-commit в папке .git/hooks/ моего проекта при помощи touch
2. написал скрипт, который проверяет файлы формата .txt на наличие в них текста
   ```
   #!/bin/bash

   if [[ $(find . -maxdepth 1 -name "*.txt" | wc -l) -eq 0 ]]; then
        echo "Нет файлов .txt для проверки"
        exit 0
   fi

   for file in *.txt; do
        if [[ ! -s "$file" ]]; then
                echo "Ошибка: файл '$file' пуст"
                exit 1
        fi
   done


   echo "Проверка пройдена успешно"
   exit 0

   ```
   3. Затем я создал пустой текстовый файл и попытался сделать commit, чтобы проверить работу скрипта![image](https://github.com/user-attachments/assets/0a2090d7-5404-4381-9e8c-4b3b98393ae3)


## Задание 2 - Использование Git Flow в проекте
 
Предположим, у вас есть задача на создание новой функциональности для вашего проекта с использованием Git Flow. Давайте рассмотрим конкретный пример. В примере важен не сам проект и его код (его тут вообще как такового нет), а принцип работы Git Flow.

1.Git Flow уже был установлен, так что я просто инициализировал его в репозитории

```
git flow init
```

2. Создал ветку для новой функциональности, с названием "task-management":

```
git flow feature start task-management
```

3. Создал файл task_manager.py и написал там функцию:

```
def create_task(title, description):
    # Логика создания задачи
    print(f"Создана новая задача: {title}")
```

4. Выполнил коммит изменения:

```
git add task_manager.py
git commit -m "Добавлен функционал управления задачами"


```

5. После завершения разработки функции завершил фичу и объединил ее с основной веткой:

```
git flow feature finish task-management

```

Git Flow автоматически переключился на ветку feature-branch и выполнил слияние. ![image](https://github.com/user-attachments/assets/695144cc-342f-4335-b17a-cb1ea807cb7e)


6. Начал создание релиза:

```
git flow release start v1.0.0
```

7. Внес изменения, связанные с релизом:

```
echo "v1.0.0" > version.txt
git add version.txt
git commit -m "Обновлена версия для релиза v1.0.0"

```

8. Завершил релиз и объединил его с ветками "feature-branch" и "main":

```
git flow release finish v1.0.0
```

9. Создал hotfix:

```
git flow hotfix start hotfix-1.0.1
```

10. Внес изменения для исправления ошибки:

```
git add file_with_error.py
git commit -m "Исправлена критическая ошибка"
```

11. Завершил hotfix и объединил его с ветками "feature-branch" и "main":

```
git flow hotfix finish hotfix-1.0.1
```

12. Завершенил работу и отправил изменения на удаленный репозиторий:

```
git push origin develop
git push origin main

```
