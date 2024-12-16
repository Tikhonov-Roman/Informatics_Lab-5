# Лабораторная работа 5
## Выполнил: Тихонов Роман Александрович К3139
### Задание 1
1) Переходим в скрытую папку hooks:
```
cd git-practice
cd .git/hooks
```
2) Создаем файл pre-commit, где будет написан скрипт для проверки коммитов:
```
touch pre-commit
gedit pre-commit
```
3) Вводим в файл следующий код:
```
#!/bin/bash

for file in $(git diff --cached --name-only); do
    if [[ $file == *.txt ]]; then
        if grep -q "Автор:" "$file"; then
            echo "Файл $file соответствует формату и имеет подпись автора."
        else
            echo "Ошибка: Файл $file соответствует формату, но не имеет подписи"
            exit 1
        fi
    else
        echo "Ошибка: Файл $file не соответствует формату!"
        exit 1
    fi
done

exit 0
```
Если  формат файла .txt, то начнётся проверка на наличие подписи автора в файле. Подпись автора имеет следующий формат "Автор:*", где *-произвольное кол-во символом. Если подпись имеется, то выполнится коммит и появится соответсвующее сообщение в консоли, если подписи нет или формат файла не .txt, то коммит прервётся и появится соответствующее собщение в консоли.
3) Возвращаемся в папку репозитория и выполняем коммит:
```
git add text.txt
git commit -m "Check pre-commit file"

```
![image](https://github.com/user-attachments/assets/ebe16551-2e75-45f5-9d74-652aba7fb2b3)
![image](https://github.com/user-attachments/assets/b0c90686-95fc-40bf-9210-f0adec089d6c)
![image](https://github.com/user-attachments/assets/6c8bf855-500c-42cb-b2a2-3027d9bf7ab5)
![image](https://github.com/user-attachments/assets/0b50dc58-a4a7-4f53-8db0-77043182e8dd)


### Задание 2 - Использование Git Flow в проекте


1. Установим Git Flow на локальную машину:

```
sudo apt-get install git-flow
```

2. В корне репозитория выполним инициализацию Git Flow.

```
git flow init
```

3. Создадим ветку для новой функциональности, допустим она называется "task-management":

```
git flow feature start task-management
```

4. Внесем изменения в код для добавления функционала управления задачами (например, в файл task_manager.py):

```
def create_task(title, description):
    # Логика создания задачи
    if description == "":
        print("Описание не задано")
    print(f"Создана новая задача: {title}")
```

Выполним коммит:

```
git add task_manager.py
git commit -m "Добавлен функционал управления задачами"
```

5. Завершим фичу и объединим ее с основной веткой:

```
git flow feature finish task-management

```

Git Flow автоматически переключится на ветку develop и выполнит слияние. 

6. Переключимся на ветку "develop" и начнем создание релиза:

```
git checkout develop
git flow release start v1.0.0
```

7. Внесем изменения, связанные с релизом (например, добавим версию в файле version.txt):

```
echo "v1.0.0" > version.txt
git add version.txt
git commit -m "Обновлена версия для релиза v1.0.0"

```


8. Завершим релиз и объединим его с ветками "develop" и "main":

```
git flow release finish v1.0.0
```

9. Создаем hotfix (у нас конечно же ошибки никакой не возникнет, но hotfix все равно создаем):

```
git flow hotfix start hotfix-1.0.1
```

10. Внесем изменения для исправления ошибки и коммитите:

```
# Исправление ошибки
git add file_with_error.py
git commit -m "Исправлена критическая ошибка"
```

11. Завершим hotfix и объединим его с ветками "develop" и "main":

```
git flow hotfix finish hotfix-1.0.1
```

12. Запушим изменения на удаленный репозиторий:

```
git push origin develop
git push origin master
```
![image](https://github.com/user-attachments/assets/c5f66628-7bdf-401c-bf7b-81f7f45df396)

