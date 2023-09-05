##### QA_templates_repository
Репозиторий для QA инженера, c различными готовыми шаблонами файлов предназначенных для работы.

--- 
### Для чего он?

Модель «общего репозитория» (The Shared Repository Model) чаще встречается у малых команд и организаций, работающих над закрытыми проектами. Каждый в команде имеет доступ «на запись» в один общий репозиторий, а для изолирования изменений применяются тематические ветви (topic branches).

Дополнительно данный репозиторий предусматривает возможность выбора настроек при инициации (добавления необходимых файлов) . Помогат сократить расходы времени, как при создании репозитория, так и при дальнейшем ведении проекта.

Вполне успешно может использоваться и в проектах с одним пользователем, при этом, дав базовые навыки понимания как может выглядить более сложный проект.

--- 
### Что в нём есть?
  +  templates/default  -  Файлы для разных целей
  +  templates/issues_yml  -  Шаблоны для заполнения issues, появляются в issues репозитория после их переноса в ветку main. Заполняются в виде форм.
  +  templates/maven  -  Файлы для работы с maven, автоматичская проверка тестов на гитхаб и настроечный pom.xml для IDEA
  +  Пустые ветки main, target, release   -  Помогают вспомнить какие ветки нужно создать при инициации репозитория, особенно в режиме создания Git Bash. Сверяя ветки templates_repository с ветками нового репозитория, можно не забыть какие из них понадобятся в работе.

--- 
### Что дальше?
  +  Пройти шаги настройки
  +  Возможно получить новые знания по командам или вспомнить забытые
  +  Задуматься о том, как выглядит проект со стороны
  +  Приучить себя к порядку
    
---
#### Шаг 1 (создать репо для работы)
1. Создать на гитхаб новый репозиторий
2. Скопировать SSH или HTTP ссылку репозитория
   +  SSH   -  ссылку на репо с методом поключения по защищенному сетевому протоколу
   +  HTTP   -  ссылку на репо с методом поключения по открытому сетевому протоколу

---
#### Шаг 2 (создать клон на рабочем столе)
1. На рабочем столе вызвать Git Bash
2. Командой  
   > git clone -o work (Shift+Insert)
   > создать клон репозитория
   
   +  git clone  -  команда клонирования  
   +  -o work  -  ключ присвоения имени новому подключению, вместо work можно своё, если не использовать ключ имя присвоится по умолчанию origin  
   +  (Shift+Insert)    -  комбинация клавиш для вставки в Git Bash из буфера обмена  
   
3. Закрыть Git Bash, либо командой  
   > cd имя_появившейся_папки  
   > перейти в папку клона
4. Снова открыть Git Bash на появившейся на рабочем столе папке репо

---
#### Шаг 3 (слинковать с другими репо)
Ожидаемый результат  -  папка репо будет иметь связь с тремя репозиториями  
  +  репозиторий с именем work, с возможностью push, в котором будет выполняться задание  
  +  репозиторий с именем target, из которого можно скопировать задание и исходники, в одну из веток work  
  +  репозиторий с именем temp, из которого можно скопировать настройки, в одну из веток work  
1. Скопировать ссылку репозитория с заданием
2. Командой  
   > git remote add target (Shift+Insert)  
   > параметры описанны в шаге про клон   
3. Скопировать ссылку репозитория с шаблонами
4. Командой  
   > git remote add temp (Shift+Insert)  
   > параметры описанны в шаге про клон  
5. Командой  
   > git remote -v  
   > убедиться что нужные репо подключенны  
6. Командой  
    > git fetch --all  
    > обновить сведения о всех репо, иначе не будет видно всех веток  

---
#### Шаг 4 (собрать ветку target репо work)
Ожидаемый результат  -  в ветке target окажется первоначальная версия задания с исходным кодом и документацией (ТЗ).  
К которой можно будет всегда обратиться не прыгая между репозиториями с заданием и работой.  
1. Командой  
   > git branch -a  
   > вывести список всех веток во всех репо  
2. Командой  
   > git checkout -b target  
   > создать и сразу перейти в ветку target репо work  
3. Командой  
   > git checkout target -- ./  
   > скопировать содержимое ветки main из репо target, в текущюю ветку target репо work  
4. Командой  
   > git add -A  
   > принять изменения в ветке target  
5. Командой  
   > git commit -m "set target"  
   > создать коммит изменений в ветке target  
6. Командой  
   > git push  
   > отправить изменения в ветку target репо work
7. Зайти в интерфейс репо work на гитхаб и заблокировать в настройках branch ветки target любые обновления этой ветки  

---
#### Шаг 5 (собрать ветку main репо work)
Ожидаемый результат  -  ветка main окажется отправной точкой всего пректа, в которую по мере исполнения задания будет мержится готовый вариант из ветки release. 
А также main превратиться в точку возврата при совсем запутанных ситуациях. Реализуется полным уничтожением release и дальнейшим востановлением из main.  
1. Командой  
   > git branch -a  
   > вывести список всех веток во всех репо  
2. Командой  
   > git checkout main
   > перейти в ветку main  
3. Командой  
   > git checkout temp/templates/default -- ./  
   > скопировать содержимое ветки templates/default из репо temp, в текущюю ветки main репо work  
4. Команд'ами  
   > git checkout temp/templates/<name> -- ./  
   > повторить копирование содержимого нужных веток templates/<name> из репо temp, в текущюю ветки main репо work  
5. Командой  
   > git add -A
   > принять изменения в текущей ветке  
6. Командой  
   > git commit -m "set main"  
   > создать коммит изменений в ветке main  
7. Командой  
   > git push  
   > отправить изменения в ветку main репо work  
8. Зайти в интерфейс репо work на гитхаб и заблокировать в настройках branch ветки main любые обновления этой ветки  

---
#### Шаг 6 (собрать ветку release репо work)
Ожидаемый результат  -  ветка release станет местом сборки различных частей проекта, в случаи успешного слияния она будет мерджится в main, а в случаи провала будет востанавливаться из отправной точки ветки main.  
1. Командой  
   > git branch -a  
   > вывести список всех веток во всех репо
2. Командой  
   > git checkout -b release  
   > создать и сразу перейти в ветку release репо work  
3. Командой  
   > git push  
   > отправить создание ветки release в репо work  
4. Зайти в интерфейс гитхаба с создать Pull requests ветки main в ветку release с коммитом "set release"  
5. Находясь в ветке release команд'ами  
   > git checkout target -- ./<dir>  
   > скопировать содержимое пап(ки)/(ок) с исходниками из ветки main репо target, в текущюю ветку release репо work <dir> - имя нужной директории  
6. Командой  
   > git commit -m "add src"  
   > создать коммит изменений в ветки release репо work  
8. Командой  
   > git push  
   > отправить изменения в ветку release репо work
   
---
#### Шаг 7 (создать topic branches ветки репо work)
Ожидаемый результат  -  все изменяемые части кода находятся в отдельных ветка, ветки для изменений начинаются от release, по мере необходимости изменения возвращаются обратно в ветку release. Количество веток определяется количеством участников задействованных в изменениях, для каждого своя ветка. При более маштабных работах можно выделить ветку на целую группу участников, которые в свою очередь создадут для себя ветки от этой.
1. Командой  
   > git branch  
   > вывести список всех веток репо work  
2. Командой  
   > git checkout -b topic-name  
   > создать и сразу перейти в ветку topic-name репо work  
3. Командой  
   > git merge release --ff  
   > это перенос изменений release в ветку topic-name  
   > ключ --ff (fast-forward)  -  во время неявного слияния не создается новых коммитов: используются только уже существующие. Суть этого слияния заключается в том, что из вливаемой ветки извлекаются несколько коммитов, а затем они применяются к последнему коммиту целевой ветки.  
4. Повторить шаги 2 и 3 для нужного количества веток
      
---
