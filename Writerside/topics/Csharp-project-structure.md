# Структура проекта C#

Мы уже немного говорили на эту тему [тут](Install-Visual-Studio-Code-in-Windows.md#csharp_files_and_folders). Сейчас мы 
немного больше углубимся в эту тему. И начнем сразу с практики. Создайте проект `ex0012_default_namespaces` в JetBrains Rider.
Проект должен быть в решении episode02.

![Создание проекта в JetBrains Rider](NameSpaces01.png){ border-effect="line"  thumbnail="true" width="700" }

В результате у вас должно получиться что-то вроде такого:

![Проекты в JetBrains Rider](NameSpaces02.png){ border-effect="line"  thumbnail="true" width="700" }

Был создан проект с операторами верхнего уровня, так как при создании мы не отметили галку **Do not user top-level statements**.

Классические программы C# до .NET 6.0 должны были использовать инструкцию `using` для импорта пространств имен включающих
стандартные библиотеки C#, такие, как например `System`.

Первые строки любого файла .cs могли выглядеть например так:

```c#
using System;
using System.Linq;
using System.Collections.Generic;
```
Как я уже говорил эти инструкции подключают к вашей программе стандартные библиотеки, которые содержат множество готовых
полезных методов, таких как например `WriteLine`, выводящих сообщение в консоль. То есть вам не надо изобретать велосипед,
а можно пользоваться уже готовым кодом, который написали для вас другие программисты.

Чтобы ваша программа могла найти метод `WriteLine`, ей надо объяснить где он находится. Это примерно как адрес дома, на 
улице и в городе. На самом деле метод `WriteLine` является частью класса `Console`, который в свою очередь входит в 
пространство имен `System`. Тут можно провести аналогию, что `System` - это город, `Console` - это улица, а `WriteLine` - 
это дом.

После подключения пространств имен, программа сама ищет класс и метод в объявленных пространствах имен.

Если бы, например, инструкции `using System` не было то, чтобы вызвать метод `WriteLine` необходимо было быть написать 
инструкцию:

```c#
System.Console.WriteLine("Hello World")
```

Согласитесь что это не очень удобно.

И по аналогии с городами, улицами и домами можно добавить. Что в разных городах могут быть улицы с одинаковыми названиями,
а так же дома с одинаковыми номерами. Помните комедию "Ирония судьбы, или С легким паром"?

Поскольку разные программисты могут для своих классов и методов выбрать одинаковые названия, то для этого были созданы 
пространства имен.

>По умолчанию, при создании проекта, никакое пространство имен для класса не назначается. 
> Даже если в файле проекта .csproj задано поле `<RootNamespace>`, оно используется для сборки (например, в именах ресурсов), 
> но не влияет на типы, которые вы объявляете в коде, если вы не указали пространство имен явно. Поэтому хорошей практикой
> является явное указание пространства имен в классах программы.
> {style="warning"}

Чтобы пользоваться методами из стандартной, или другой подключенной библиотеки, необходимо импортировать её пространство
имен.

В случае стандартной библиотеки входящей в SDK достаточно просто команды `using` с указанием пространства имен. 

В случае сторонней библиотеки необходим как сам файл библиотеки, так и команда `using`.

**Начиная с .NET 6.0 и соответственно с версии языка C#10 любые проекты используют неявный глобальный импорт некоторых пространств имен.**

Список неявно импортируемых пространств имен зависит от типа создаваемого проекта (шаблона). Про шаблоны мы кстати тоже говорили [тут](how-to-crate-csharp-windows-command-line.md#template_list).

Кроме того появилась инструкция `global using`, которая позволяет импортировать пространство имен только в одном файле .cs, и оно будет 
доступно во всех файлах .cs проекта.

## Неявный глобальный импорт пространств имен

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

Файл проекта **ex0012_default_namespaces.csproj** - это файл в формате XML.

>XML (eXtensible Markup Language) — это текстовый формат для хранения данных, который легко читается как человеком
>, так и компьютером. Если говорить простыми словами, XML — это способ структурировать информацию в виде текста с
> использованием тегов, похожих на HTML, но с возможностью создавать свои собственные теги.
{style="note"}

![Удаляем не нужные global using](NameSpaces07.png){ border-effect="line"  thumbnail="true" width="700" }

С помощью тегов `Using Remove` в группе `ItemGroup` мы удалили не нужные нам неявные глобальные импорты.

Сохраните файл проекта, и посмотрите как изменился файл **ex0012_default_namespaces.GlobalUsings.g.cs**:

![Удаляем не нужные global using](NameSpaces08.png){ border-effect="line"  thumbnail="true" width="700" }

Для контрольного выстрела, перейдите в файл Program.cs и снова кликните по фигурным скобкам. Вы должны увидеть следующее:

![Удаляем не нужные global using](NameSpaces09.png){ border-effect="line"  thumbnail="true" width="700" }

Запустите программу и убедитесь что она работает. Как это сделать можете вспомнить [тут](Install-JetBrains-Rider-in-Windows.md#rider_run).

Хотя если в решении несколько проектов, то для запуска нужного проекта надо его выбрать. Сделать это в JetBrains Rider
можно несколькими способами.

**Способ №1**

В верхнем правом углу выберите нужны проект и нажмите кнопку старта:

![Запускаем выбранные проект в Rider](NameSpaces10.png){ border-effect="line"  thumbnail="true" width="700" }

**Способ №2**

Щёлкните правой кнопкой мышки по проекту и выберите его запуск:

![Запускаем выбранные проект в Rider](NameSpaces11.png){ border-effect="line"  thumbnail="true" width="700" }

**Способ №3**

Нажмите сочетание клавиш `Ctrl+Alt+Shift+R` и выберите проект для запуска:

![Запускаем выбранные проект в Rider](NameSpaces12.png){ border-effect="line"  thumbnail="true" width="700" }

## Отключение неявного глобального импорта для проекта
Согласитесь, что если вам в консольном приложении не нужны все эти библиотеки, то писать для удаления каждой отдельный тэг
это не очень весело. К тому же в других шаблонах библиотек может быть гораздо больше. И удалять каждую поодиночке не очень.

Убрать неявный импорт можно либо вообще удалив элемент `<ImplicitUsings>enable</ImplicitUsings>`, или изменить его значение
на `disable`, то есть привести его к виду `<ImplicitUsings>disable</ImplicitUsings>`. А затем импортировать только нужные
пространства имен.

Давайте попрактикуемся в этом и создадим проект **ex0013_disable_default_namespace** в VSCode. Если забыли как это делать 
почитайте [тут](Install-Visual-Studio-Code-in-Windows.md#c-vscode).

Откройте файл проекта **ex0013_disable_default_namespace.csproj** и приведите его к виду и сохраните:

```XML
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net8.0</TargetFramework>
    <ImplicitUsings>disable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>

  <ItemGroup>
    <Using Include="System.Console" Static="true" />
    <Using Include="System.Environment" Alias="Env" />
  </ItemGroup>

</Project>
```

У вас должно получится что-то вроде такого:

![Проект в VSCode](NameSpaces13.png){ border-effect="line"  thumbnail="true" width="700" }

Откройте терминал в папке проекта и дайте команду `dotnet clean`, чтобы изменения точно применились к файлу неявного
глобального импорта. А затем посмотрите содержимое файла **ex0013_disable_default_namespace.GlobalUsings.g.cs**. Оно
должно быть таким:

```C#
// <auto-generated/>
global using Env = global::System.Environment;
global using static global::System.Console;
```

![Проект в VSCode](NameSpaces14.png){ border-effect="line"  thumbnail="true" width="700" }

Теперь измените код файла Program.cs на следующий:

```C#
WriteLine($"Операционная система: {System.Runtime.InteropServices.RuntimeInformation.OSDescription}");
WriteLine($"Текущая директория: {Env.CurrentDirectory}");
WriteLine("Имя класса: {0}", typeof(Program).Name);
WriteLine("Имя пространства имён класса: {0}", typeof(Program).Namespace);
WriteLine("Полное имя: {0}", typeof(Program).FullName);
WriteLine($"Имя компьютера {Env.MachineName}");
```
И запустите программу:

![Проект в VSCode](NameSpaces15.png){ border-effect="line"  thumbnail="true" width="700" }

Как видите команда:

```c#
WriteLine("Имя пространства имён класса: {0}", typeof(Program).Namespace);
```

выводит пустую строку, потому что в коде не определено пространство имён.

Если вы помните и видите, то данная программа использует операторы верхнего уровня.

>Задать пространство имен для программы с операторами верхнего уровня (top-level statements) в C# невозможно. 
> В этом случае компилятор автоматически создает класс Program без явного назначения пространства имен, и все операторы 
> верхнего уровня находятся в глобальном пространстве имен.
{style="warning"}

Обратите внимание на вывод программы. Хотя мы не задавали имя класса, оно было создано автоматически.

В C# инструкции должны находится в каком-либо классе. Давайте попытаемся узнать в каком методе находятся инструкции нашей 
программы. Для этого чуток её изменим добавив всего одну строку в нашу программу:

```C#
WriteLine($"Текущий метод: {System.Reflection.MethodBase.GetCurrentMethod()?.Name}");
```
Теперь снова запустим нашу программу:

![Проект в VSCode](NameSpaces16.png){ border-effect="line"  thumbnail="true" width="700" }

Как видим метод в котором находятся все инструкции программы называется `<Main>$`.

Почему это происходит?

Когда вы используете операторы верхнего уровня, компилятор C#:

- Создает класс Program автоматически.
- Помещает код операторов верхнего уровня в метод `<Main>$`.
- Не присваивает этот класс какому-либо пространству имен, даже если используется директива namespace.

Когда вы используете операторы верхнего уровня (то есть пишете код без явного объявления метода Main), компилятор 
автоматически создаёт метод Main, чтобы правильно скомпилировать и запустить программу. Однако он добавляет к названию 
дополнительные символы, чтобы отличить этот метод от обычного метода Main, написанного вручную.

Имя метода `<Main>$` указывает на то, что это метод был автоматически сгенерирован компилятором при использовании 
операторов верхнего уровня.

Операторы верхнего уровня (Top-level statements) были введены в C# 9.0, чтобы сделать язык проще и более удобным, 
особенно для начинающих разработчиков и в сценариях, когда нужно написать простой или небольшой скрипт. 
Рассмотрим основные цели и преимущества этого нововведения.

### 1. **Упрощение создания простых программ**
До введения операторов верхнего уровня даже для написания простого "Hello, World!" в C# требовалось создавать класс и метод `Main`. Пример до C# 9:

```c#
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```

С появлением операторов верхнего уровня этот код стал проще:

```c#
Console.WriteLine("Hello, World!");
```

Теперь можно писать код без явного объявления класса и метода `Main`, и он будет работать сразу.

### 2. **Улучшение читаемости кода**
Для небольших скриптов и тестов операторы верхнего уровня улучшают читаемость, поскольку они убирают лишние конструкции:

- Не нужно создавать отдельный класс.
- Не нужно явно писать метод `Main`.
- Нет необходимости использовать дополнительные директивы `using` (включены по умолчанию, если включены **Implicit Usings**).

Пример: создание и вывод списка чисел.
```c#
var numbers = new List<int> { 1, 2, 3, 4, 5 };
numbers.ForEach(Console.WriteLine);
```

### 3. **Ускорение написания кода**
Для небольших утилит, скриптов или обучающих примеров операторы верхнего уровня позволяют быстрее писать код. Они полезны для:

- Сниппетов и демонстрационного кода.
- Быстрого прототипирования.
- Сценариев автоматизации (например, при написании небольших консольных утилит).

### 4. **Уменьшение объёма кода шаблона**
При создании нового проекта `.NET Console` теперь создаётся файл с использованием операторов верхнего уровня, что упрощает процесс разработки, особенно если целью является просто быстрое выполнение задачи.

Пример кода в файле `Program.cs` по умолчанию:
```c#
Console.WriteLine("Hello, World!");
```

### 5. **Снижение порога входа для начинающих**
Для новых пользователей C# стандартный шаблон программы с классом и методом `Main` может казаться сложным и избыточным. Операторы верхнего уровня делают язык более доступным, позволяя писать код без лишних деталей, которые могут быть непонятны начинающим.

### Примечания и ограничения:
1. **Ограничение на один файл с операторами верхнего уровня** — в проекте может быть только один файл, использующий операторы верхнего уровня.
2. **Инициализация и использование зависимостей** — при использовании операторов верхнего уровня сложнее организовать сложные зависимости и конфигурацию, которые обычно делаются в методе `Main` или через DI-контейнеры.
3. **Подходит для простых проектов** — при создании более сложных и больших проектов рекомендуется использовать традиционный подход с классом и методом `Main` для лучшей структурированности.

Операторы верхнего уровня делают язык C# более гибким и удобным для простых сценариев и задач, улучшая опыт написания кода и 
снижая количество шаблонного кода, необходимого для запуска программы. Они идеально подходят для быстрого написания скриптов 
и прототипов, но в больших проектах по-прежнему актуален классический подход с явным определением метода `Main`.

Как видите за кулисами может происходить много вещей о которых нужно знать. Поэтому зри в корень, падаван!

Теперь давайте создадим проект без операторов верхнего уровня, чтобы все таки вывести информацию о пространстве имен.

## Включение явного глобального импорта для проекта

Для на начала мы установим один полезный шаблон для создания консольного приложения. Этот шаблон импортирует только одно
пространство имен из стандартной библиотеки, необходимое для вывода сообщений в консоль.

Этот шаблон полезен тем, что больше ни кто не будет делать работу за вас и вы будете делать всё сами. 
Соответственно получая опыт и понимание от куда у всего растут ноги. В общем мы отказываемся на первом этапе от помощи 
невидимок, чтобы научиться видеть и понимать процессы происходящие под капотом в приложении .NET.

Но у этого шаблона есть и одно полезное приемущество о котором мы поговорим чуть позже. Итак, ближе к делу, падаван!

Последовательно дайте команды

```
dotnet new install TinyConsoleTemplate.CSharp::1.0.8
dotnet new --list | find "Tiny"
```
Первая из них устанавливает шаблон, второй мы убеждаемся что он появился в списке доступных шаблонов для создания приложения.

![Установка шаблона](NameSpaces17.png){ border-effect="line"  thumbnail="true" width="700" }

Вы так же можете посмотреть справку по этому шаблону командой `dotnet new tinyconsole --help`.

Теперь в командной строке в подкаталоге episode02 создадим проект x0014_global_using командой: