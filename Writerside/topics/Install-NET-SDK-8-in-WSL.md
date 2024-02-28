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

![WSL Ubuntu в меню Старт](wsl_ubuntu03.png){border-effect="line"}

Если версия WSL начинается c цифры 2, то все ок. Если с цифры 1, [то вам надо переключиться на версию 2](https://learn.microsoft.com/ru-ru/windows/wsl/install#check-which-version-of-wsl-you-are-running).

В принципе у вас уже должен быть запущен терминал с Ubuntu. Вы можете запустить еще один. Это нормальная практика когда
в Linux запущено несколько терминалов.

Запустить еще один терминал Ubuntu вы можете из меню "Пуск"

![WSL Ubuntu в меню Старт](wsl_ubuntu02.png){border-effect="line"}

Кликните по иконке Ubuntu. Запуститься консоль Ubuntu:

![WSL Ubuntu в меню Старт](wsl_ubuntu04.png){border-effect="line"}

Закройте консоль Ubuntu.

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
