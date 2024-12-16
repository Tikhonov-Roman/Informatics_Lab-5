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


### Задание 2
