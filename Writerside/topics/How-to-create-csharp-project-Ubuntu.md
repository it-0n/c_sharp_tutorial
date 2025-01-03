# Создание проекта C# в WSL Ubuntu

Собственно нет ни какой разницы в какой ОС создавать проекты C#. В командной строке это делается абсолютно одинаково во
всех ОС. Но все же один проект создадим просто для практики.

Запустите терминал Ubuntu. По идее у вас уже должна быть символьная ссылка на каталог с проектами, которые мы делали.
Давайте перейдем в каталог проектов первого эпизода командой:

`cd it0n/episode01`

И создадим консольный проект без операторов верхнего уровня с названием **ex0005_hello_os**, как обычно, командой:

`dotnet new console -o ex0005_hello_os --use-program-main`

И перейдем в каталог с проектом командой `cd ex0005_hello_os`

![Создание консольного проекта C# в командной строке Ubuntu](ex0005_01.png){border-effect="line" thumbnail="true" width="621"}

Откройте файл Program.cs в редакторе nano командой:

`nano Program.cs`

После того как откроется редактор приведите программу к следующему виду:

![Редактирование программы C# в редакторе nano](ex0005_02.png){border-effect="line" thumbnail="true" width="621"}

После того как закончите редактировать сохраните код нажав `Ctrl+o` и выйдите из редактора нажав `Ctrl+x`.

> Если вам будет сложно редактировать код в редакторе nano, то можете это сделать и в любом текстовом редакторе Windows.
{style="note"}

Запустите эту программу в терминале Ubuntu, а затем в командной строке Windows. Вы должны увидеть следующее:

![Запуск в Ubuntu](ex0005_03.png){border-effect="line"}

![Запуск в Windows](ex0005_04.png){border-effect="line"}

> Пусть вас не смущает значок Ubuntu на последнем скриншоте, если вы присмотритесь, то увидите что на самом деле 
> активной вкладкой в Windows Terminal является вкладка командной строки (Command Prompt) Windows.
{style="note"}

Обратите внимание, что вывод при запусках в разных ОС разный. Эту магию делает как раз та длинная загадочная строка.
Выглядит как магическое заклинание 😊 Ничего! Скоро вы овладеете этой магией.

Хотя если вы внимательно прочитаете эту длинную строку кода, то сможете примерно догадаться что она делает.

Хочу заметить, что на данном этапе мы даже не начали изучать программирование. Мы сразу начали практиковаться. К тому
времени как начнем изучать C# у вас уже будет хороший опыт, который вам сильно поможет в изучение C#. По крайней мере
к этому моменту вы уже должны уметь легко создавать консольные проекты C# в командной строке, а это уже большое дело.