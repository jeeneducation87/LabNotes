# Домашнее задание к занятию «Ветвления в Git»

### Цель задания

В процессе работы над заданием вы потренеруетесь делать merge и rebase. В результате вы поймете разницу между ними и научитесь решать конфликты.   

Обычно при нормальном ходе разработки выполнять `rebase` достаточно просто. 
Это позволяет объединить множество промежуточных коммитов при решении задачи, чтобы не засорять историю. Поэтому многие команды и разработчики предпочитают такой способ.   


### Инструкция к заданию

1. В личном кабинете отправьте на проверку ссылку на network графика вашего репозитория.
2. Любые вопросы по решению задач задавайте в разделе "Вопросы по заданию".


### Дополнительные материалы для выполнения задания

1. Тренажёр [LearnGitBranching](https://learngitbranching.js.org/), где можно потренироваться в работе с деревом коммитов и ветвлений. 

------

### Создание скриптов

`mkdir branching`
`code branching/merge.sh`
`code branching/rebase.sh`
- Сохраняем код в оба файла

![alt text](image.png)

- Фиксируем изменения
`git add branching/`
`git commit -m "prepare for merge and rebase"`
`git push origin main`

![alt text](image-1.png)

### Ветка git-merge

- Создаем ветку

`git checkout -b git-merge`

- Открываем branching/merge.sh и меняем "$*" на "$@" и echo "\$* ..." на echo "\$@ ...":

![alt text](image-2.png)

- Коммит изменений:

`git add branching/merge.sh`
`git commit -m "merge: @ instead *"`
`git push origin git-merge`

![alt text](image-3.png)

- Снова меняем branching/merge.sh:

![alt text](image-4.png)
 

- Коммит изменений:
 
`git add branching/merge.sh`
`git commit -m "merge: use shift"`
`git push origin git-merge`

![alt text](image-5.png)


###  Изменение main

- Возвращаемся в main:

`git checkout main`

![alt text](image-6.png)

- Меняем файл branching/rebase.sh:

![alt text](image-7.png)  

- Коммит изменений:

`git add branching/rebase.sh`
`git commit -m "update rebase.sh in main"`
`git push origin main`

![alt text](image-8.png)

### Ветка git-rebase

- Ищем хеш коммита "prepare for merge and rebase":
     
`git log --oneline`

![alt text](image-9.png)

- Переключаемся на хеш (c2f43f3, который стоит напротив сообщения "prepare for merge and rebase") и создаем ветку:
    
`git checkout c2f43f3`
`git checkout -b git-rebase`

![alt text](image-10.png)

- Меняем branching/rebase.sh:

![alt text](image-11.png)

- Коммит изменений:
     
`git add branching/rebase.sh`
`git commit -m "git-rebase 1"`

![alt text](image-12.png)

- Снова меняем branching/rebase.sh (меняем echo внутри цикла на echo "Next parameter: $param"):

![alt text](image-13.png)

- Коммит изменений:
     
`git add branching/rebase.sh`
`git commit -m "git-rebase 2"`
`git push -u origin git-rebase`

![alt text](image-15.png)

- Смотрим что получили в репозитории GitHub (Network):

![alt text](image-16.png)

### Merge (слияние)

- Переходим в main и сливаем ветку git-merge:
    
`git checkout main`
`git merge git-merge`
`git push origin main`

![alt text](image-18.png)

### Rebase

- Переходим в ветку git-rebase:

`git checkout git-rebase`

- Запускаем интерактивный rebase на main:

`git rebase -i main`

![alt text](image-19.png)

- Видим конфликт №1:

![alt text](image-20.png)

- Оставляем echo "\$@ Parameter #$count = $param"

![alt text](image-21.png)

   
`git add branching/rebase.sh`
`git rebase --continue`

- Конфликт №2: Снова конфликт. Оставляем строку echo "Next parameter: $param" :

![alt text](image-22.png)     

`git add branching/rebase.sh`
`git rebase --continue`

![alt text](image-23.png)

- Push с силой (-f): Обычный push не сработает, так как мы переписали историю.

`git push -u origin git-rebase -f`

![alt text](image-24.png)

### Финальное слияние

![alt text](image-25.png)

`git checkout main`
`git merge git-rebase`
`git push`

![alt text](image-26.png)

![alt text](image-27.png)

Ссылки на репозиторий: 
[GitHub](https://github.com/jeeneducation87/devops-netology/tree/main)
