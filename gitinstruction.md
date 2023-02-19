![Сюда загрузится моё фото](face.jpg)
# Работа с Git и GitHub
## Работа с Git
### 1. Проверка наличия установленного Git
В терминале (командной строке) необходимо выполнить команду `git --version`
Если Git установлен, то появится сообщение с информацией о версии программы. Иначе будет сообщение об ошибке.

Если Git установлен, то переходим к пункту 3, если нет - к следующему.

### 2. Установка Git и VisualStudio Code
Загружаем последнюю версию Git из https://git-scm.com/downloads и устанавливаем с настройками по умолчанию.

Загружаем последнюю версию VisualStudio Code из https://code.visualstudio.com/download и устанавливаем с настройками по умолчанию. *Прим. Версию для Windows 7 скачиваем из https://code.visualstudio.com/updates/v1_70*

### 3. Первый запуск Git из VisualStudio Code
Запускаем VisualStudio Code и в левом верхнем углу выбираем (или создаём) каталог, в котором мы будем работать с файлами проекта. Создаем в нём файл.

Для работы с Git'ом необходимо сообщить ему имя и контакные данные пользователя, который будет работать с ним.

Для этого сообщаем Git'у: 
1. Ваше имя выполнеием команды `git config --global user.name «Ваше имя английскими буквами»`
1. Ваш электронный адрес - `git config --global user.email ваша почта@example.com`

### 4. Инициализация репозитория
Переходим в терминал и проверяем наличи репозитория в данной папке выполнением команды `git status` 

Выдача результата: _"fatal: not a git repository (or any of the parent directories): .git"_ показывает отсутствие репозитория.

Создаем репозиторий командой `git init`

### 5. Запись изменений в репозиторий
Запись изменнений осуществуляется в два этапа:
1. Подготовка изменений, которые необходимо сохранить в репозиторий.
1. Помещение подготовленных изменений в репозиторий (коммит).

Подготовить изменения можно командой `git add file_name`. Данная команда универсальная и позволяет подготовить как создание нового файла, так и изменения в файле, который уже помещался в репозиторий ранее.

Команда `git add .` подготавливает к помещению в репозиторий все изменения, которые были выполнены с момента последнего коммита.

Коммит осуществляется выпонением команды `git commit`. Так как помещение текущей версии файла(ов) в репозиторий осуществляется для возможности лёгкого перемещения между версиями, то к каждому коммиту пишут сообщение, в котором описывают произведённые изменения и отличия от предыдущей версии. Это достигается использованием опертора "-m". Полностью это выглядит так: `git commit -m "Сообщение или комментарий"`

> [!TIP]
> Можно объединить подготовку изменений и помещение их в репозиторий в одной команде: `git commit -am "Сообщение или комментарий"` Стоит учитывать, что данная команда не сможет добавить новые файлы в репозиторий, а только изменения в файлах, уже отслеживаются Git'ом.

### 6. Просмотр истории коммитов

Осуществляется командой `git log`
Могут применяться операторы:
* --oneline
* --graph

Целиком команда может выглядеть 
* так `git log --online` 
* или так `git log --graph`
* или даже так `git log --oneline --graph`

### 7. Перемещение между сохранениями (версиями)

Осуществляется командой `git checkout code_of_commit`

Код коммита (code_of_commit) - это буквенно-цифровое обозначение, которое присваивается программой Git и видно в верхней строке каждого коммита, список которых (историю) можно вывести командой `git log`

### 8. Игнорирование файлов

Чтобы исключить из отслеживания в репозитории определенные файл(ы) и/или папки, необходимо создать там файл ***.gitignore*** и записать в него их названия и/или шаблоны, соответствующие таким файлам и/или папкам.

### 9. Создание веток в Git
Ветка в Git - это указатель на один из коммитов, обычно последний в цепочке коммитов.
По умолчанию имя первой (основной) ветки - **master**

Создать новую ветку можно командой `git branch new_branch_name`
При этом активной останется существующая ветка.

Создать новую ветку и сразу перейти в неё (сделать её активной) можно командой `git checkout -b create_branche`

Список существующих веток вызывается командой `git branch`

Перемещение между веток (обращение к ним) производится командой `git checkout имя_существующей_ветки`, например `git checkout master`

### 10. Слияние веток и разрешение конфликтов
Для слияния ветки branch_name с текущей веткой выполнется команда `git merge branch_name`

Если была изменена одна и та же строка(и) в обеих ветках тогда может возникнуть конфликт слияния, который потребует участия пользователя. После разрешения конфликта необходимо сделать коммит для фиксации тех изменений, на которых мы остановились.

### 11. Удаление веток
Ветку, которая уже слита с другой веткой можно удалить командой `git branch -d имя_слитой_ветки`.

При попытке удалить таким образом ветку с уникальными коммитами приведёт к ошибке и команда не будет выполнена.

Если неслитую ветку всё таки нужно удалить, то воспользуйтесь командой `git branch -D имя_ветки`

### 12. Отмена и удаление коммитов

git reset HEAD~ # удаляем только коммит
git reset --hard HEAD~ # удаляем коммит и изменения
А вот отменить изменения сделанные в последнем коммите можно с помощью команды git revert. Она делает еще один коммит, но с противоположными изменениями.

git revert aa600a43cb164408e4ad87d216bc679d097f1a6c
*нужно передать ей хеш коммита, который мы отменяем*


## Работа с удалёнными репозиториями (GitHub)

На примере GitHub - это один из сервисов для групповой работы с Git-репозиториями, предоставляется Microsoft.

Реализуется две схемы работы: со своим репозиторием или с чужим(и).

В любом случае необходимо создать свой аккаунт на GitHub.

### 1. Работа со своим репозиторием

Сначала создаём удалённый репозиторий на GitHub.

Сразу после его создания GitHub предложит три способа его инициализации: 
1. создать новый локальный репозиторий, подготовить и отправить его в GitHub;
1. подготовить существующий локальный репозиторий и отправить его в GitHub;
1. импортировать в GitHub код из другого репозитория.

В первых двух случаях будет необходимо пройти авторизацию Git'a в GitHub.

В GitHub'е основная ветка наызвается main, поэтому основную ветку в Git'е нужно назвать также (или переименовать).

Созданным репозиторием можно поделиться через ссылку.

Связь между локальным и удаленным репозиториями устанавливается командами ...

Обмен коммитами между локальным и удаленным репозиториями происходит через две команды: 
* push - отправляет данные в удалённый репозиторий;
* pull - загружает данные в локальный репозиторий и делает слияние репозиториев.

### 2. Работа с чужим репозиторием
Сначала создаём ветвление от исходного репозитория в свой аккаунт на GitHub (fork).

Затем создаём локальную копию fork'а командой 
```
git clone repozitory_url
```
После её выполнения создается новая папка внутри которой выполнялась команда clone, поэтому далее необходимо сменить рабочую папку для Git'a.

Фактически мы создаём новый (свой, локальный) репозиторий из существующего удалённо.

Все изменения, которые мы хотим предложить автору проекта, создаются в новой ветке!

После фиксации изменений отправляем обновлённый проект в свой профиль на GitHub командой `git push origin new_branch_name`. 

После обновления страницы в браузере появится кнопка "Compare and pull request", которая позволяет нам предложить наши изменения в проект его автору.

### Полезные команды

  Вывести список псевдонимов удалённых репозиториев в Git'е - `git remote`

Добавить удалённый репозиторий к проекту (в Git'е):
```
git remote add repozitory_name repozitory_url
```
`git push origin new_branch_name`

`git push -u origin main`

## Полезные ссылки:

Git-тренажёр: `https://learngitbranching.js.org/`