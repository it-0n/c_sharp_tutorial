# Структура проекта C#

Мы уже немного говорили на эту тему [тут](Install-Visual-Studio-Code-in-Windows.md#csharp_files_and_folders). Сейчас мы 
немного больше углубимся в эту тему. И начнем сразу с практики. Создайте проект `ex0012_default_namespaces` в JetBrains Rider.
Проект должен быть в решении episode02.

![Создание проекта в JetBrains Rider](NameSpaces01.png){ border-effect="line"  thumbnail="true" width="700" }

В результате у вас должно получиться что-то вроде такого:

![Проекты в JetBrains Rider](NameSpaces02.png){ border-effect="line"  thumbnail="true" width="700" }

Теперь мы посмотрим какие пространства имен (namespaces) были импортированы нашей программой. Кстати это мы уже делали
[тут](how-to-crate-csharp-windows-command-line.md#RiderDefaultNamespace). Рекомендую освежить это в памяти.

На скриншоте выше вы видите фигурные скобки в области нумерации строк у первой строки. Наведите на нее мышь.

![Проекты в JetBrains Rider](NameSpaces03.png){ border-effect="line"  thumbnail="true" width="700" }

Вы должны увидеть подсказку **Global 'using' directives**. Как раз о глобальном явном и неявном импортах мы сейчас и будем
говорить.

Далее кликните по этим фигурным скобкам мышкой. И вы должны увидеть следующее:

![Проекты в JetBrains Rider](NameSpaces04.png){ border-effect="line"  thumbnail="true" width="700" }

Ну можно сказать преступление раскрыто! Мы вышли на след файла где неявно импортируются пространства имен. Этот файл
создается в подкаталоге obj/Debug/net8.0 во время создания проекта автоматически. Имя файла всегда стандартное. 
Сперва идет имя проекта, потом точка, а за ним **GlobalUsings.g.cs**.

Давайте посмотрим на этот файл и его сообщников. Для этого кликнем в правом верхнем углу по стрелке вниз рядом со словом 
Solution и выберем File system. 

![Проекты в JetBrains Rider](NameSpaces05.png){ border-effect="line"  thumbnail="true" width="700" }

Далее разверните каталоги obj/Debug/net8.0 и откройте в редакторе файл **ex0012_default_namespaces.GlobalUsings.g.cs**.

![Проекты в JetBrains Rider](NameSpaces06.png){ border-effect="line"  thumbnail="true" width="700" }

И вот они наши голубчики неявные импорты где порылися. Но для простого консольного приложения выводящего одну строку
многие из этих библиотек не нужны. Давайте уберем не нужные. Но хочу напомнить, что этот файл создается автоматически.
Поэтому нам надо отредактировать файл нашего проекта **ex0012_default_namespaces.csproj** и привести его к следующему виду:

```xml
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>net8.0</TargetFramework>
        <ImplicitUsings>enable</ImplicitUsings>
        <Nullable>enable</Nullable>
    </PropertyGroup>

    <ItemGroup>
        <Using Remove="System.Threading" />
        <Using Remove="System.Collections.Generic" />
        <Using Remove="System.Linq" />
        <Using Remove="System.Net.Http" />
        <Using Remove="System.Threading" />
        <Using Remove="System.Threading.Tasks" />
    </ItemGroup>

</Project>
```

![Удаляем не нужные global using](NameSpaces07.png){ border-effect="line"  thumbnail="true" width="700" }

Сохраните файл проекта, и посмотрите как изменился файл **ex0012_default_namespaces.GlobalUsings.g.cs**:

![Удаляем не нужные global using](NameSpaces08.png){ border-effect="line"  thumbnail="true" width="700" }

Для контрольного выстрела, перейдите в файл Program.cs и снова кликните по фигурным скобкам. Вы должны увидеть следующее:

![Удаляем не нужные global using](NameSpaces09.png){ border-effect="line"  thumbnail="true" width="700" }

Запустите программу и убедитесь что она работает. Как это сделать можете вспомнить [тут](Install-JetBrains-Rider-in-Windows.md#rider_run).

