# Обновление .NET SDK в WSL
Пока писал статьи для курса приехали обновления для .NET 8.0, поэтому решил сразу же показать как обновлять .NET в WSL.
В курсе, по крайней мере, в его начальной версии мы использовали Ubuntu как основную систему в WSL. Поэтому примеры
будут приводиться для неё. Но возможно курс будет дополнен примерами и для других дистрибутивов Linux.

Поскольку установка .NET в Linux (WSL) может быть сделана несколькими способами, то и способы обновления соответственно
будут разные.

## Обновление .NET в варианте установки из репозитория Ubuntu
Этот вариант установки .NET мы использовали как самый простой. Собственно и обновление для этого варианта самое простое.

Откройте терминал Ubuntu и дайте следующие команды:

`sudo apt update`

`apt list --upgradable`

>Версии .NET которые вы увидите, могут отличаться от тех что на скриншоте. Поскольку время идет. Выходят новые версии.
{style="note"}

![Обновление .NET SDK 8 в WSL Ubuntu](dotnetUbuntuUpdate01.png){border-effect="line" thumbnail="true" width="700"}

Я подсветил версии пакета .NET 8.0 SDK, чтобы вы смогли увидеть с какой и на какую версию будет обновлён .NET SDK 8.0.
Но так же будут обновлены и другие пакеты .NET. Посмотрите внимательно сами.

Дайте команду `dotnet --info`, чтобы посмотреть текущую версию .NET ещё раз.

![Обновление .NET SDK 8 в WSL Ubuntu](dotnetUbuntuUpdate02.png){border-effect="line" thumbnail="true" width="700"}

Для обновления дайте команду `sudo apt upgrade -y`, которая обновит все доступные для обновления пакеты Ubuntu, в том числе
и пакеты .NET. Этой займет какое-то время пока пакеты буду скачаны из сети и установлены.

![Обновление .NET SDK 8 в WSL Ubuntu](dotnetUbuntuUpdate03.png){border-effect="line" thumbnail="true" width="700"}

Затем снова дайте команду `dotnet --info` чтобы, посмотреть какая версия .NET стала после обновления.

![Обновление .NET SDK 8 в WSL Ubuntu](dotnetUbuntuUpdate04.png){border-effect="line" thumbnail="true" width="700"}

Как видите версия .NET повысилась. Обновление завершено.