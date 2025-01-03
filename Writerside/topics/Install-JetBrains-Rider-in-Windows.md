# Установка JetBrains Rider в Windows и проверка работы
JetBrains Rider c 24 октября 2024 года [стал бесплатным](https://blog.jetbrains.com/blog/2024/10/24/webstorm-and-rider-are-now-free-for-non-commercial-use/) для не коммерческого использования.

Продукты компании JetBrains можно установить двумя способами: 
- Установка каждого продукта отдельно
- Установка с помощью JetBrains Toolbox

Мы рассмотрим первый вариант.

Скачиваем Rider [тут](https://www.jetbrains.com/ru-ru/rider/download/), запускаем и жмём **Next**.

![Установка JetBrains Rider в Windows](InstallJetBrainsWindows01.png){ border-effect="line"}

>Картиночки для разных версий JetBrains Rider могут меняться.
{style = note}

Выбираем расположение установки и жмем **Next**.

![Установка JetBrains Rider в Windows](InstallJetBrainsWindows02.png){ border-effect="line"}

Оставляем все по умолчанию и жмем **Next**.

![Установка JetBrains Rider в Windows](InstallJetBrainsWindows03.png){ border-effect="line"}

И наконец **Install**.

![Установка JetBrains Rider в Windows](InstallJetBrainsWindows04.png){ border-effect="line"}

![Установка JetBrains Rider в Windows](InstallJetBrainsWindows05.png){ border-effect="line"}

После окончания установки закрываем окно, оставив галку отмеченной чтобы Rider сразу же запустился.

![Установка JetBrains Rider в Windows](InstallJetBrainsWindows06.png){ border-effect="line"}

## Создание решения и консольного проекта в Rider с операторами верхнего уровня {id="how-to-create-solution-in-rider"}
При первом запуске вам зададут пару вопросов.

Ставим соглашалку и жмем **Continue**.

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows01.png){ border-effect="line"}

Здесь жмите что хотите.

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows02.png){ border-effect="line"}

Если у вас установлена Visual Studio, то вам предложат скопировать горячие клавиши Visual Studio и недавние проекты.
Как видите на скриншоте я не стал этого делать. Вы можете поступать как посчитаете нужным. Всё это можно настроить и позже.

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows03.png){ border-effect="line"}

Далее вам предложат выбрать цветовую схему. Выбирайте и жмите **Next**.

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows04.png){ border-effect="line"}

И ещё раз спросят про горячие клавиши. Сделайте как на скриншоте и жмите **Next**.

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows05.png){ border-effect="line"}

Да давайте уже запустим Rider. Жмите **Start JetBrains Rider**! Плагины потом поставите если будет надо.

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows06.png){ border-effect="line"}

Выберите **Start trial**, и нажмите **Start trial**.

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows07.png){ border-effect="line"}

Блин! Ну когда же оно запуститься?! Жмите **Continue**

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows08.png){ border-effect="line"}

Жмём **New Solution**

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows09.png){ border-effect="line"}

Далее, в разделе .NET / .NET Core, выбираем Console Application и заполняем поля названия решения и проекта, а так же
правильно выбираем директорию. Как будет выглядеть структура каталогов и файлов проекта и решения можно видеть чуть 
ниже всех настроек. После того как правильно введёте все нужные данные жмите кнопку **Create**.

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows10.png){ border-effect="line"}

{id="rider_run"} Rider создаст решение и проект и вы должны увидеть что-то вроде этого:

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows11.png){ border-effect="line"  thumbnail="true" width="700"}

Закройте окно **AI Assistant** и запустите проект на исполнение. В результате вы должны получить что-то вроде этого:

![Первое приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows12.png){ border-effect="line"  thumbnail="true" width="700"}

Поздравляю! Вы запустили приложение в Rider!

## Добавление в решение консольного проекта в Rider без операторов верхнего уровня {id="rider_add_project_to_solution"}
Теперь добавим второй проект консольного приложения без операторов верхнего уровня. Для этого нажмите на названии решения
правой кнопкой мыши и выберите **Add** и затем **New Project...** или нажмите `Ctrl+Shift+N`.

![Второе приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows13.png){ border-effect="line"  thumbnail="true" width="700"}

Выберите создание консольного приложения, заполните поля как на скриншоте и жмите **Create**.

![Второе приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows14.png){ border-effect="line"  thumbnail="true" width="700"}

Приведите код к виду как показано на скриншоте и запустите проект, предварительно выбрав его для запуска в раскрывающемся
списке. Вы должны получить что-то вроде этого:

![Второе приложение в JetBrains Rider в Windows](FirstProjectJetBrainsWindows15.png){ border-effect="line"  thumbnail="true" width="700"}

Поздравляю! Вы добавили в решение второй проект и запустили его!!

## Работа в Rider с проектами в WSL {id="Rider_and_WSL"}
В Rider есть, так же как и в VSCode, есть возможность работы с WSL. Закройте и заново запустите Rider. Вы должны увидеть 
список предыдущих проектов, а так же возможность запуска работы с WSL.

![Работа в Rider в WSL](RiderWSL01.png){ border-effect="line"  thumbnail="true" width="700"}

Выберите в раскрывающемся списке **Connect to host...**

![Работа в Rider в WSL](RiderWSL02.png){ border-effect="line"  thumbnail="true" width="700"}

И затем Ubuntu и нажмите **Next**

![Работа в Rider в WSL](RiderWSL03.png){ border-effect="line"  thumbnail="true" width="700"}

Rider начнёт запускать WSL и подготавливать её к работе.

![Работа в Rider в WSL](RiderWSL04.png){ border-effect="line"  thumbnail="true" width="700"}

![Работа в Rider в WSL](RiderWSL05.png){ border-effect="line"  thumbnail="true" width="700"}

Затем вам надо будет выбрать проект в WSL, нажмите на плюсик

![Работа в Rider в WSL](RiderWSL06.png){ border-effect="line"  thumbnail="true" width="700"}

Rider опять задумается на некоторое время

![Работа в Rider в WSL](RiderWSL07.png){ border-effect="line"  thumbnail="true" width="700"}

И далее вам надо будет выбрать файл решения

![Работа в Rider в WSL](RiderWSL08.png){ border-effect="line"  thumbnail="true" width="700"}

Выберите файл решения **ex0008_JetBrainsRider_solution.sln**

![Работа в Rider в WSL](RiderWSL09.png){ border-effect="line"  thumbnail="true" width="700"}

И нажмите Download IDE and Connect (или же сами скачайте дистрибутив, как это сделать читайте чуть ниже)

Вам надо будет дождаться пока Rider скачает IDE Backend (полный дистрибутив Rider для Linux) и запустит его в WSL. 
Конечно 1,5Гб впечатляют. Но это, ещё разок, полный дистрибутив Rider который будет устанавливаться в WSL.

![Работа в Rider в WSL](RiderWSL13.png){ border-effect="line"}

Если вы устанете ждать или загрузка зациклиться, то можно сделать проще. Отменить загрузку нажав **Cancel**
Пойти на [сайт JetBrains](https://www.jetbrains.com/ru-ru/rider/download/#section=linux)
и скачать дистрибутив Rider самим.

![Работа в Rider в WSL](RiderWSL26.png){ border-effect="line"   thumbnail="true" width="700"}

После того как скачаете дистрибутив, в окне **Choose IDE and Project** жмёте на **Installation options...** и выбираете
**Upload installer file**

![Работа в Rider в WSL](RiderWSL27.png){ border-effect="line"   thumbnail="true" width="700"}

Далее выбираете скачанный дистрибутив и путь к файлу решения и жмете **Upload IDE and Connect**

![Работа в Rider в WSL](RiderWSL15.png){ border-effect="line"   thumbnail="true" width="700"}

Далее начнется загрузка IDE (Rider) на WSL, его установка и запуск

![Работа в Rider в WSL](RiderWSL16.png){ border-effect="line"   thumbnail="true" width="700"}

![Работа в Rider в WSL](RiderWSL17.png){ border-effect="line"   thumbnail="true" width="700"}

Вас попросят согласиться с лицензией. Ставим галку и жмём **Continue**

![Работа в Rider в WSL](RiderWSL18.png){ border-effect="line"   thumbnail="true" width="700"}

Затем, скорее всего вам снова придется подключиться к WSL. Прямо квест какой-то!

![Работа в Rider в WSL](RiderWSL19.png){ border-effect="line"   thumbnail="true" width="700"}

Будет происходить подключение...

![Работа в Rider в WSL](RiderWSL20.png){ border-effect="line"   thumbnail="true" width="700"}

И затем вы должны увидеть установленный в WSL Rider скачанной вами версии. Выбираете ещё раз файл решения
и жмете **Start IDE and Connect**

![Работа в Rider в WSL](RiderWSL21.png){ border-effect="line"   thumbnail="true" width="700"}

Ещё раз соглашаетесь с лицензией. Когда же это закончиться?! А?!

![Работа в Rider в WSL](RiderWSL22.png){ border-effect="line"   thumbnail="true" width="700"}

Тут жмем **Get Started**

![Работа в Rider в WSL](RiderWSL23.png){ border-effect="line"   thumbnail="true" width="700"}

И, наконец, не веря своему счастью, вы видите запущенный в WSL Rider!!! Аллилуя! Аллах Акбар! Харе Кришна! Слава Богу!
Мы наконец таки запустили Rider в WSL.

![Работа в Rider в WSL](RiderWSL24.png){ border-effect="line" thumbnail="true" width="700"}

Дальше всё просто! Выбираем файл в проекте и запускаем его, как вы это уже делали.

![Работа в Rider в WSL](RiderWSL25.png){ border-effect="line" thumbnail="true" width="700"}

Фсё! Если вы это сделали, то молодец!

Потом уже запускать Rider в WSL будет прощё. 

Ещё раз хочу отметить, что в WSL была установленна полноценная версия Rider. И в принципе вы это так же могли бы
сделать на удаленной машине, установив Rider или другую IDE JetBrains, по ssh. И потом удаленно работать с кодом
используя мощности удаленной машины. Это круто. И весь этот квест стоил того чтобы его пройти.

## Работа в Rider с проектами удаленно по SSH в Linux {id="Rider_and_SSH"}

>Внимание! Чтобы проделать это упражнение у вас уже должен быть установлен Ubuntu Server 22.04 на виртуальной или реальной
>удаленной машине, и так же, на сервере уже должен быть установлен .NET SDK 8.0.
{style = note}

Пример я буду показывать на виртуальном сервере Ubuntu 22.04. Виртуальная машина имеет IP 192.168.10.22.
Давайте туда сперва закинем директорию с нашими проектами. Для этого можно использовать встроенный в Windows 10 клиент
ssh. И так копируем всю структуру каталогов с проектами на удаленную машину. Команду `scp` выполняете на своей машине.

`scp -r it0nCS\ itpro@192.168.10.22:/home/itpro`

После выполнения этой команды в домашнем каталоге пользователя itpro будет создан каталог itOnCS.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote01.png){ border-effect="line"}

Теперь будем устанавливать удаленно Rider. Скачанный дистрибутив у нас уже есть. Запускаем Rider и выбираем
всё как на скриншоте.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote02.png){ border-effect="line"  thumbnail="true" width="700"}

Далее жмём на шестеренку и создаём новое подключение по SSH.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote03.png){ border-effect="line"  thumbnail="true" width="700"}

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote04.png){ border-effect="line"  thumbnail="true" width="700"}

Вводим данные для подключения, тестируем соединение и сохраняем введенные данные.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote05.png){ border-effect="line"  thumbnail="true" width="700"}

После этого выбираем созданное подключение и жмём **Check Connection and Continue**

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote06.png){ border-effect="line"  thumbnail="true" width="700"}

Если получили такое предупреждение до докиньте памяти на машинку и подключитесь снова. На виртуалке это делается за пару секунд.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote07.png){ border-effect="line"  thumbnail="true" width="700"}

Подключаемся снова. И жмем на плюс, чтобы добавить проект.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote08.png){ border-effect="line"  thumbnail="true" width="700"}

Рядом с плюсом есть значок терминала, если по нему кликнуть то откроется эмулятор терминала и вы подключитесь к удаленной машине.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote09.png){ border-effect="line"  thumbnail="true" width="700"}

Это было справочно-лирическое отступление от темы. И так мы жмём плюс и затем выбираем **Installation options...** и выбираете
**Upload installer file**. 

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote10.png){ border-effect="line"  thumbnail="true" width="700"}

Выбираем наш скачанный дистрибутив и жмём **Upload IDE and Connect**

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote11.png){ border-effect="line"  thumbnail="true" width="700"}

Странно, но нас ещё раз попросят ввести пароль.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote12.png){ border-effect="line"  thumbnail="true" width="700"}

И затем начнётся загрузка и установка дистрибутива Rider на Ubuntu Server 22.04.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote13.png){ border-effect="line"  thumbnail="true" width="700"}

И затем уже откроется Rider.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote14.png){ border-effect="line"  thumbnail="true" width="700"}

Открываем наш проект и запускаем его, как мы это уже несколько раз делали.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote15.png){ border-effect="line"  thumbnail="true" width="700"}

Если вы всё это смогли проделать, то вы молодец, падаван!

Когда Rider подключен удаленно, то можно наблюдать за загрузкой процессора, памяти и размером дисков на удаленной машине.

![Работа в Rider по SSH удаленно с Linux Ubuntu](RiderLinuxRemote16.png){ border-effect="line"  thumbnail="true" width="700"}

## Обновление Rider в WSL или на удаленной машине Linux

>Внимание! Этот раздел может вам понадобиться если вы обновили Rider на своём компе, но не обновили его в WSL или на 
> удаленном компьютере.
{style = note}

Если версия Rider установленного на вашем компьютере больше чем версия Rider установленного в WSL или на удаленной машине,
то вам придется обновить Rider в WSL или на удаленной машине. Такое может произойти если вы локально у себя на компе обновили
Rider, а в WSL или на удаленной машине этого не сделали. Rider вам предложит скачать более новую версию с сайта JetBrains,
а затем вам надо будет установить ее в WSL или на удаленном компьютере.

Например, после локального обновления Rider, откройте проект в WSL или на удаленной машине. И вы увидите примерно следующее:

![Обновление Rider в WSK](RiderWSLUpdate01.png){ border-effect="line"  thumbnail="true" width="700"}

Выберите пункт **Select Different IDE...**, после чего вы должны увидеть примерно следующее:

![Обновление Rider в WSK](RiderWSLUpdate02.png){ border-effect="line"  thumbnail="true" width="700"}

Обратите внимание, что Rider предложит вам опцию, что он сам скачает нужную версию и установит её, но иногда он валиться 
на этом. Поэтому скачайте с сайта JetBrains новую версию (с таким же номером как локально установленная).

Нажмите на **Installation options...** и выберите **Upload Installer file...**

![Обновление Rider в WSK](RiderWSLUpdate03.png){ border-effect="line"  thumbnail="true" width="700"}

После этого укажите путь к скачанному дистрибутиву Rider и нажмите **Upload IDE and connect

![Обновление Rider в WSK](RiderWSLUpdate04.png){ border-effect="line"  thumbnail="true" width="700"}

Далее вы увидите что Rider загружает и устанавливает новую версию Rider в WSL из дистрибутива, который вы ранее скачали.

После установки новой версии Rider в WSL жмите **Connect to WSL** и открывайте нужный проект, как мы делали это выше.

![Обновление Rider в WSK](RiderWSLUpdate05.png){ border-effect="line"  thumbnail="true" width="700"}
