# Установка .NET SDK 8 в WSL
[WSL](https://learn.microsoft.com/ru-ru/windows/wsl/) или [Windows Subsystem for Linux](https://learn.microsoft.com/ru-ru/windows/wsl/faq) -
это функция операционной системы Windows, которая позволяет запускать файловую
систему Linux, а также программы командной строки Linux и приложения графического пользовательского интерфейса
непосредственно в Windows, наряду с традиционными классическими приложениями и приложениями Windows.

Простыми словами это возможность запустить полноценный Linux внутри Windows. То есть вы можете работать одновременно и в Windows,
и в Linux на вашем компьютере. Здорово же?

Чтобы воспользоваться [WSL в Windows его сперва надо установить](https://learn.microsoft.com/ru-ru/windows/wsl/install).

## Установка WSL
Установка WSL очень простая. В командной строке запущенной с правами Администратора надо дать команду:

`wsl --install`

Эта команда включит функции, необходимые для запуска WSL и установит Ubuntu. **После окончания работы
этой команды перезагрузите компьютер.**

Скриншоты работы команды:

![WSL install on Windows](wsl_install01.png){border-effect="line"}

![WSL install on Windows](wsl_install02.png){border-effect="line"}

![WSL install on Windows](wsl_install03.png){border-effect="line"}

Всё очень просто! Неправда ли?

Значок Ubuntu должен появиться в меню "Старт" ещё до перезагрузки компьютера. Не щёлкайте по нему. Просто перезагрузите комп.

![WSL Ubuntu в меню Старт](wsl_ubuntu01.png){border-effect="line"}

После перезагрузки откроется консоль Windows и вы увидите следующий этап установки WSL:

![WSL install on Windows](wsl_install04.png){border-effect="line"}

Затем вам предложат задать имя пользователя Ubuntu и его пароль.

>Когда вы будете вводить пароль, то вводимые вами символы отображаться не будут.
{style="note"}

![WSL install on Windows](wsl_install05.png){border-effect="line"}

После того как вы подтвердите пароль Ubuntu будет полностью готова к работе. Сейчас вы видите консоль Ubuntu. Хотя
внешне она может выглядеть **почти** так же как консоль Windows.

>Не путайте консоль Ubuntu с консолью Windows. Отличить вы можете по символу приглашения к вводу команд. В Windows это
> как правило знак **>**, а в Linux, как правило, знак **$**.
{style="note"}

## Проверка версии WSL и запуск консоли Ubuntu {id="wsl_1"}
Чтобы проверить установленную версию WSL в **командной строке Windows** дайте команду:

`wsl -v`

![Проверка версии WSL](wsl_ubuntu03.png){border-effect="line"}

Если версия WSL начинается c цифры 2, то все ок. Если с цифры 1, [то вам надо переключиться на версию 2](https://learn.microsoft.com/ru-ru/windows/wsl/install#check-which-version-of-wsl-you-are-running).

В принципе у вас уже должен быть запущен терминал с Ubuntu. Вы можете запустить еще один. Это нормальная практика когда
в Linux запущено несколько терминалов.

Запустить еще один терминал Ubuntu вы можете из меню "Пуск"

![WSL Ubuntu в меню Старт](wsl_ubuntu02.png){border-effect="line"}

Кликните по иконке Ubuntu. Запуститься консоль Ubuntu:

![WSL запуск Ubuntu из меню Старт](wsl_ubuntu04.png){border-effect="line"}

Так же, если у вас установлен Windows Terminal, там тоже появиться возможность запустить терминал Ubuntu.

![WSL Ubuntu в Windows Terminal](wsl_ubuntu05.png){border-effect="line" thumbnail="true" width="621"}

Вы можете запустить Ubuntu и в Windows Terminal.

![WSL Ubuntu в Windows Terminal](wsl_ubuntu06.png){border-effect="line" thumbnail="true" width="621"}

Закройте все консоли Ubuntu. Мы будем обновлять ядро WSL.

## Обновление ядра WSL {id="wsl_2"}
Запустите **командную строку Windows** с правами администратора и дайте следующую команду:

`wsl --update`

Если есть обновления, то начнется обновление ядра WSL.

![WSL install on Windows](wsl_install06.png){border-effect="line"}

После обновления проверьте версию WSL уже знакомой вам командой:

`wsl -v`

![WSL install on Windows](wsl_install07.png){border-effect="line"}

Сравните номер версии при первом запуске этой команды и после обновления.

>Номера версий у вас могут быть другие. Всё течёт, всё меняется.
{style="note"}

## Обновление Ubuntu
Запустите терминал Ubuntu и дайте там команду

`sudo apt update && sudo apt upgrade -y`

![WSL обновление Ubuntu](wsl_ubuntu07.png){border-effect="line"}

У вас спросят пароль от учетной записи, который вы создали после перезагрузки компа, когда устанавливали WSL.
Введите пароль и нажмите Enter.

>Во время ввода пароль отображаться не будет.
{style="note"}

![WSL обновление Ubuntu](wsl_ubuntu08.png){border-effect="line"}

Далее Ubuntu начнёт обновляться. Почувствуйте себя кул хацкером из фильмов про кул хацкеров :)

Дождитесь обновления Ubuntu

![WSL обновление Ubuntu](wsl_ubuntu09.png){border-effect="line"}

## Установка .NET SDK в WSL Ubuntu
[Установка .NET SDK в Linux и в частности в Ubuntu возможна несколькими способами](https://learn.microsoft.com/ru-ru/dotnet/core/install/linux-ubuntu).
Мы воспользуемся самым простым.

Запустите терминал Ubuntu, если он у вас еще не был запущен и дайте там следующую команду

`sudo apt install dotnet-sdk-8.0 -y`

>Данная команда установки точно будет работать в Ubuntu 22.04, и возможно более поздних версиях.
> Уточняйте в документации Microsoft.
{style="note"}

![Установка .NET SDK 8 в WSL Ubuntu](wsl_ubuntu_SDK8_install01.png){border-effect="line" thumbnail="true" width="621"}

Вас снова попросят ввести пароль. Привыкайте к этому в Linux. После ввода пароля жмите Enter и начнется установка
.NET SDK 8.

![Установка .NET SDK 8 в WSL Ubuntu](wsl_ubuntu_SDK8_install02.png){border-effect="line" thumbnail="true" width="621"}

Дождитесь окончания установки .NET SDK 8. И затем дайте команду:

`dotnet --info`

![Установка .NET SDK 8 в WSL Ubuntu](wsl_ubuntu_SDK8_install03.png){border-effect="line" thumbnail="true" width="621"}

Чтобы посмотреть какие версии .NET SDK и .NET Runtime были установлены.

Поздравляю! Вы установили .NET SDK 8 в Ubuntu.

## Запуск программы C# в WSL Ubuntu
Давайте сразу же запустим программу из первого упражнения которую мы написали в разделе создания проектов под Windows.

В терминале Ubuntu дайте команду:

`cd /mnt/d/it0nCS/episode01/ex0001_hello_world && ls`

![Переход в каталог для запуска программы C# в WSL Ubuntu](wsl_dotnetrun01.png){border-effect="line"}

Этой командой мы перешли в каталог приложения ex0001_hello_world и посмотрели его содержимое.

>Если вы создали каталог на диске С, то команда должна быть другой.
> 
> `cd /mnt/c/it0nCS/episode01/ex0001_hello_world && ls`
{style="note"}

Теперь запустим нашу программу уже известной нам командой `dotnet run`

![Запуск программы C# в WSL Ubuntu](wsl_dotnetrun02.png){border-effect="line"}

>При первом запуске программы .NET поприветствует вас и выдаст уведомление об установке сертификата разработчика.
> 
>Дайте команду `dotnet run` ещё раз и этого уведомления уже больше не будет.
{style="note"}

Как видите, чтобы запустить нашу программу под Linux в ней ни чего не пришлось менять.

В качестве первого задания данной статьи будет запуск проекта **ex0002_main_hello_cs** в Ubuntu. Вам надо перейти в
каталог проекта и запустить программу. Вперед, падаван! И да пребудет с тобой сила!

Результат должен выглядеть так:

![Запуск второй программы C# в WSL Ubuntu](wsl_dotnetrun03.png){border-effect="line"}

>На скриншоте выше путь к каталогу размыт. Не путайте это с пробелами. Посмотрите на предыдущий скриншот.
> Используйте команду `cd` для перехода в каталог **ex0002_main_hello_cs**.
> Считайте это подсказкой для выполнения первого задания.
{style="note"}

Как видите и кириллица выводится правильно в Linux. Опять же мы не делали ни каких изменений в программе, а просто
запустили её. Это и означает кроссплатформенность.

## Пользователям VMWare Workstation
Поскольку для работы WSL нужна виртуализация, то для этого используется Hyper-V встроенный в Windows 10. Несколько лет
назад одновременная установка на компьютере VMWare Workstation и Hyper-V приводила к полной поломке VMWare Workstation.
Сейчас эта проблема практически исправлена, но всё же при запуске виртуальной машины в VMWare Workstation вы можете получить
следующее предупреждение:

![VMWare Workstation выдает предупреждение если запущено на компьютере с установленным Hyper-V](vmwareworkstation01.png){border-effect="line"}

Производительность виртуальной машины будет снижена и бла бла бла. И так же там сеть [ссылка на решение проблемы](https://kb.vmware.com/s/article/79832).

Исправляется это просто установкой галки **Disable Side Channel Mitigations for Hyper-V enabled host** в свойствах виртуальной
машины:

![Запуск второй программы C# в WSL Ubuntu](vmwareworkstation03.png){border-effect="line"  thumbnail="true" width="621"}

Если же вы решите установить VMWare Workstation уже после того как установили WSL, то при установке получите вот такое сообщение:

![Запуск второй программы C# в WSL Ubuntu](vmwareworkstation02.png){border-effect="line"}

Чекните указанную галку и продолжайте установку.
