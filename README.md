# Домашнее задание к занятию "Системы контроля" - Морозоа Александр

В файле terraform/.gitignore перечислены файлы которые не будут добавлены в Commit:
1. Все файлы с расширением ".tfvars", ".tfvars.json"
3. Файл с именем ".terraform.tfstate.lock.info", ".terraformrc", "terraform.rc"

Tag v0.1

### Цель задания

В результате выполнения задания вы: 

* научитесь подготоваливать новый репозиторий к работе;
* сохранять, перемещать и удалять файлы в системе контроля версий.  


### Чеклист готовности к домашнему заданию

1. Установлена консольная утилита для работы с Git.


### Инструкция к заданию

1. Домашнее задание выполните в GitHub-репозитории. 
2. В личном кабинете отправьте на проверку ссылку на ваш репозиторий с домашним заданием.
3. Любые вопросы по решению задач задавайте в чате учебной группы.


### Дополнительные материалы для выполнения задания

1. [GitHub](https://github.com/).
2. [Инструкция по установке Git](https://git-scm.com/downloads).
3. [Книга про  Git на русском языке](https://git-scm.com/book/ru/v2/) - рекомендуем к обязательному изучению главы 1-7.
   
   
------

## Задание 1. Создать и настроить репозиторий для дальнейшей работы на курсе

В рамках курса вы будете писать скрипты и создавать конфигурации для различных систем, которые необходимо сохранять для будущего использования. 
Сначала надо создать и настроить локальный репозиторий, после чего добавить удалённый репозиторий на GitHub.

### Создание репозитория и первого коммита

1. Зарегистрируйте аккаунт на [https://github.com/](https://github.com/). Если предпочитаете другое хранилище для репозитория, можно использовать его.
2. Создайте публичный репозиторий, который будете использовать дальше на протяжении всего курса, желательное с названием `devops-netology`.
   Обязательно поставьте галочку `Initialize this repository with a README`. 
   
    ![Диалог создания репозитория](img/github-new-repo-1.jpg)

    Созданный репозиторий `devops-netology`

    ![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/1.png)

3. Создайте [авторизационный токен](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) для клонирования репозитория.

Сгенерированный токен:

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/2.png)

4. Склонируйте репозиторий, используя протокол HTTPS (`git clone ...`).
 
    ![Клонирование репозитория](img/github-clone-repo-https.jpg)

Склонированный репозиторий

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/3.png)
    
5. Перейдите в каталог с клоном репозитория (`cd devops-netology`).
6. Произведите первоначальную настройку Git, указав своё настоящее имя, чтобы нам было проще общаться, и email (`git config --global user.name` и `git config --global user.email johndoe@example.com`). 
7. Выполните команду `git status` и запомните результат.

Статус Git
![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/4.png)

8. Отредактируйте файл `README.md` любым удобным способом, тем самым переведя файл в состояние `Modified`.
9. Ещё раз выполните `git status` и продолжайте проверять вывод этой команды после каждого следующего шага. 

Статус после отредактированного файла `README.md`
![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/5.png)

10. Теперь посмотрите изменения в файле `README.md`, выполнив команды `git diff` и `git diff --staged`.

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/6.png)

11. Переведите файл в состояние `staged` (или, как говорят, просто добавьте файл в коммит) командой `git add README.md`.
12. И ещё раз выполните команды `git diff` и `git diff --staged`. Поиграйте с изменениями и этими командами, чтобы чётко понять, что и когда они отображают. 

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/7.png)

13. Теперь можно сделать коммит `git commit -m 'First commit'`.
14. И ещё раз посмотреть выводы команд `git status`, `git diff` и `git diff --staged`.

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/8.png)

### Создание файлов `.gitignore` и второго коммита

1. Создайте файл `.gitignore` (обратите внимание на точку в начале файла), проверьте его статус сразу после создания. 

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/9.png)

2. Добавьте файл `.gitignore` в следующий коммит (`git add...`).
3. На одном из следующих блоков вы будете изучать `Terraform`, давайте сразу создадим соотвествующий каталог `terraform` и внутри этого каталога — файл `.gitignore` по примеру: https://github.com/github/gitignore/blob/master/Terraform.gitignore.  

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/10.png)

4. В файле `README.md` опишите своими словами, какие файлы будут проигнорированы в будущем благодаря добавленному `.gitignore`.
5. Закоммитьте все новые и изменённые файлы. Комментарий к коммиту должен быть `Added gitignore`.

### Эксперимент с удалением и перемещением файлов (третий и четвёртый коммит)

1. Создайте файлы `will_be_deleted.txt` (с текстом `will_be_deleted`) и `will_be_moved.txt` (с текстом `will_be_moved`) и закоммите их с комментарием `Prepare to delete and move`.

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/11.png)

2. В случае необходимости обратитесь к [официальной документации](https://git-scm.com/book/ru/v2/Основы-Git-Запись-изменений-в-репозиторий) — здесь подробно описано, как выполнить следующие шаги. 
3. Удалите файл `will_be_deleted.txt` с диска и из репозитория. 

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/12.png)

4. Переименуйте (переместите) файл `will_be_moved.txt` на диске и в репозитории, чтобы он стал называться `has_been_moved.txt`.
5. Закоммитьте результат работы с комментарием `Moved and deleted`.

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/13.png)

### Проверка изменения

1. В результате предыдущих шагов в репозитории должно быть как минимум пять коммитов (если вы сделали ещё промежуточные — нет проблем):
    * `Initial Commit` — созданный GitHub при инициализации репозитория. 
    * `First commit` — созданный после изменения файла `README.md`.
    * `Added gitignore` — после добавления `.gitignore`.
    * `Prepare to delete and move` — после добавления двух временных файлов.
    * `Moved and deleted` — после удаления и перемещения временных файлов. 
2. Проверьте это, используя комманду `git log`. Подробно о формате вывода этой команды мы поговорим на следующем занятии, но посмотреть, что она отображает, можно уже сейчас.

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/14.png)

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/15.png)

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/16.png)

### Отправка изменений в репозиторий

Выполните команду `git push`, если Git запросит логин и пароль — введите ваши логин и пароль от GitHub. 

![alt text](https://github.com/Mars12121/devops-netology/blob/main/img/17.png)

В качестве результата отправьте ссылку на репозиторий. 

----

### Правила приёма домашнего задания

В личном кабинете отправлена ссылка на ваш репозиторий.


### Критерии оценки

Зачёт:

* выполнены все задания;
* ответы даны в развёрнутой форме;
* приложены соответствующие скриншоты и файлы проекта;
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

* задание выполнено частично или не выполнено вообще;
* в логике выполнения заданий есть противоречия и существенные недостатки
