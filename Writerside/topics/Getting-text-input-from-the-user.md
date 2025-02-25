# Получаем текстовый ввод в C#

Получить текстовый ввод от пользователя в консольных приложениях можно двумя способами:
- через метод [Console.ReadLine()](https://learn.microsoft.com/ru-ru/dotnet/api/system.console.readline)
- через аргументы командной строки

Далее мы подробно на примерах рассмотрим метод `Console.ReadLine()` и немного познакомимся со способом получения ввода 
через аргументы командной строки.

## Как спросить у пользователя его имя и возраст?

Если вы хотите спросить у пользователя что-то и получить от него ответ, в C# это делается с помощью метода `Console.ReadLine()`.
Он ждёт, пока пользователь что-то напечатает, а потом возвращает это в виде строки, когда нажата клавиша **Enter**.

Пример:

```c#
Console.Write("Введите своё имя и нажмите Enter: ");
string? firstName = Console.ReadLine();

Console.Write("Введите свой возраст и нажмите Enter: ");
string? age = Console.ReadLine();

Console.WriteLine($"Привет, {firstName}! Ты выглядишь отлично для {age} лет.");
```

### Важно: `Console.ReadLine()` всегда возвращает строку!

>Обратите внимание, что вводимые данные **всегда** воспринимаются как строка (`string`). Даже если вы вводите число, 
> например "25", программа всё равно считает его текстом. Это важно, если вам нужны числа для расчетов.
> {style="warning"}

## Что делать, если нужны числа?

Так как `Console.ReadLine()` возвращает строку, её нужно **преобразовать** в число, если мы хотим работать с числами. 
Для этого есть специальные методы. Вот некоторые из них:

- `Convert.ToInt32()` – преобразует строку в целое число (`int`).
- `Convert.ToDouble()` – преобразует строку в число с плавающей точкой (`double`).
- `Convert.ToDecimal()` – для работы с деньгами (`decimal`).

Пример с числами:

```c#
Console.Write("Введите свой возраст: ");
int age = Convert.ToInt32(Console.ReadLine());

Console.Write("Введите свой рост в метрах (через запятую): ");
double height = Convert.ToDouble(Console.ReadLine());

Console.WriteLine($"Возраст: {age} лет, рост: {height} м.");
```

### Важно: в разных странах разные разделители!

В русской локализации для дробных чисел используется **запятая** (например, `1,75`), а в английской – **точка** (`1.75`). 
Если программа выдаёт ошибку при вводе дробного числа, попробуйте использовать нужный разделитель. 
Или делайте дополнительные проверки и преобразуйте строку так как вам нужно и затем её обрабатывайте.

Но тут есть ещё одна проблема: если ввести что-то кроме цифр (например, "двадцать" или "15a"), программа сломается и 
выдаст ошибку. Поэтому надо **проверять ввод перед конвертацией**!

### Проверяем, что введена строка состоящая только из целочисленных цифр

Используем `int.TryParse()`, который возвращает `true`, если строка содержит только цифры, и `false`, если в ней есть 
что-то лишнее.

```c#
Console.Write("Введите ваш возраст: ");
string? input = Console.ReadLine();

if (int.TryParse(input, out int age))
{
    Console.WriteLine($"Вам {age} лет.");
}
else
{
    Console.WriteLine("Ошибка: возраст должен быть числом!");
}
```

### Проверка ввода для `double` и `decimal`

Для работы с числами с плавающей точкой (`double`, `decimal`) тоже нужно использовать `TryParse()`, но с учётом разделителя 
(точка или запятая):

```c#
Console.Write("Введите ваш рост (например, 1.75): ");
string? input = Console.ReadLine();

if (double.TryParse(input, out double height))
{
    Console.WriteLine($"Ваш рост: {height} м.");
}
else
{
    Console.WriteLine("Ошибка: введите корректное число!");
}
```

Здесь важно учитывать локализацию системы: в русской ОС вводится запятая (`1,75`), в английской — точка (`1.75`).

## Пустое значение в `ReadLine()` {id="readline_null"}

Метод `Console.ReadLine()` может вернуть `null`, если вдруг ввод невозможен (например, ввод идёт из файла, а файл закончился) 
или пользователь на запрос строки просто нажал Enter. Так что можно подстраховаться и написать так:

```c#
string? name = Console.ReadLine();
if (name == null)
{
    Console.WriteLine("Ошибка ввода!");
}
```

Также можно использовать оператор `!`, если вы уверены, что ввод **точно** будет:

```c#
string name = Console.ReadLine()!; // Говорим компилятору "не волнуйся, null не будет"
```

## Аргументы командной строки как альтернатива `ReadLine()`

Иногда удобнее передавать данные в программу сразу при запуске. Это делается через аргументы командной строки. 
Вот простой пример:

```c#
class Program
{
    static void Main(string[] args)
    {
        if (args.Length > 0)
        {
            Console.WriteLine($"Привет, {args[0]}!");
        }
        else
        {
            Console.WriteLine("Имя не введено!");
        }
    }
}
```

Запуск такой программы в терминале:

```
dotnet run Иван
```

Выведет:
```
Привет, Иван!
```

Этот метод вам станет более понятным когда мы изучим циклы, условные выражения и массивы.

Практика, падаван!

Создай консольное приложение `ex0075_user_input` при помощи шаблона `tinyconsole` в папке `episode02` и добавь его в
файл решения `episode02.sln`. Это можно сделать как в командной строке, так и в любой IDE.

Приведи Program.cs к следующему виду:

```c#
using System.Globalization;

class Program
{
    static void Main(string[] args)
    {
        string name = null;
        int? age = null;
        double? height = null;

        // Обработка аргументов командной строки
        if (args.Length >= 1)
            name = args[0];

        if (args.Length >= 2 && int.TryParse(args[1], out int parsedAge))
            age = parsedAge;

        if (args.Length >= 3 && TryParseHeight(args[2], out double parsedHeight))
            height = parsedHeight;

        // Запрос недостающих данных у пользователя
        if (string.IsNullOrWhiteSpace(name))
        {
            Write("Введите ваше имя: ");
            name = ReadLine();
        }

        while (age == null)
        {
            Write("Введите ваш возраст (целое число): ");
            string input = ReadLine();
            if (int.TryParse(input, out parsedAge))
                age = parsedAge;
            else
                WriteLine("Ошибка: Введите корректное целое число.");
        }

        while (height == null)
        {
            Write("Введите ваш рост (число с дробной частью): ");
            string input = ReadLine();
            if (TryParseHeight(input, out parsedHeight))
                height = parsedHeight;
            else
                WriteLine("Ошибка: Введите корректное число (разделитель - точка или запятая).");
        }

        // Вывод данных
        WriteLine("\nВы ввели:");
        WriteLine($"Имя: {name}");
        WriteLine($"Возраст: {age}");
        WriteLine($"Рост: {height:F2}");
    }

    // Метод для парсинга числа с дробной частью в независимости от культуры
    static bool TryParseHeight(string input, out double result)
    {
        return double.TryParse(input, NumberStyles.Float, CultureInfo.InvariantCulture, out result) ||
            double.TryParse(input, NumberStyles.Float, new CultureInfo("ru-RU"), out result);
    }
}
```

### Как работает программа:
1. Проверяет аргументы командной строки (`args`).
2. Если аргументы не указаны или указаны не все, запрашивает недостающие данные через `Console.ReadLine()`.
3. Гарантирует, что возраст — это целое число.
4. Корректно парсит рост, поддерживая `.` и `,` в качестве разделителей. Парсинг делается с помощью метода `TryParseHeight`, который мы сами написали.
5. Если при вводе возраста или роста просто нажать Enter, то программа будет повторять запрос пока не будет введено верное значение.
6. Выводит собранные данные.

### Примеры запуска:
#### 1. Через командную строку:
```sh
dotnet run Иван 25 1.85
```
**Вывод:**
```
Вы ввели:
Имя: Иван
Возраст: 25
Рост: 1.85
```
---
#### 2. Частично через командную строку, остальное вводится вручную:
```sh
dotnet run Иван
```
(Запросит возраст и рост)
```
Введите ваш возраст (целое число): 30
Введите ваш рост (число с дробной частью): 1,80
Вы ввели:
Имя: Иван
Возраст: 30
Рост: 1.80
```

Программа универсальна и будет работать независимо от настроек культуры в системе. 

На заметку. Видите метод `TryParse` у `int` и `double`? Вспоминайте, C# до мозга костей объектно-ориентированный язык.

Встроенные типы в C# содержат много полезных пасхальных яичек 😊

Так же обратите внимание, что у этой программы уже два метода:
- `Main()` - является точкой входа в программу. С этого метода начинается выполнение программы.
- `TryParseHeight()` - метод который мы сами написали, для корректного парсинга строк, содержащих вещественные числа.

И тут вам есть ещё один подарочек от шаблона `tinyconsole`. Вам не надо каждый раз писать `Console.ReadLine()`. 
Достаточно писать `ReadLine()`. В C# много всяких ништяков которые вы можете использовать. Главное знать о них 😎

Знание - сила! Не знание - рабочая сила. Выбирай, падаван, на какой стороне силы ты будешь 😊

Кстати, падван, ни какое дежавю тебя не посетило? Помнишь что в [самых первых упражнениях](how-to-crate-csharp-windows-command-line.md#0003) 
ты делал уже [это](how-to-crate-csharp-windows-command-line.md#0004)?

Там мы даже подробнее разбирали [метод получения данных от пользователя через командную строку](how-to-crate-csharp-windows-command-line.md#0003).
И лишь слегка коснулись метода [ReadLine()](how-to-crate-csharp-windows-command-line.md#0004).

Повторенье - мать ученья 😊

В качестве задания, попробуйте запускать программу различными способами:
- без аргументов
- с одним, двумя и тремя аргументами
- на некоторые вопросы нажимать Enter
- попробуйте не ввести имя и посмотреть что будет
- попробуйте найти ошибки, не учтенные варианты ввода в программе

Если сможете, исправьте программу так, чтобы она запрашивала имя пользователя если оно не было введено до тех пор, пока
пользователь его не введет. Вы можете посмотреть как это сделано для роста и возраста.

Да, мы пока не изучали условные операторы и циклы, но это мы уже узнаем в следующих разделах. Поэтому можете вернуться
к этому заданию когда узнаете про эти операторы.

### Итог

- `Console.ReadLine()` – простой способ получить текст от пользователя.
- Все данные приходят в виде строк, числа надо **конвертировать**.
- Будьте внимательны с дробными числами – запятая или точка?
- Можно передавать данные при запуске программы через аргументы командной строки.

Теперь, падаван, ты готов писать свои крутые консольные программы 🚀 с получением ввода от пользователя 🧑‍💻!

## Бонус!

Поскольку далее мы часто будем использовать пользовательский ввод в программах, то давайте упростим себе жизнь!

Как вы уже поняли, чтобы задать пользователю вопрос для получения от него данных надо сперва восопользоваться методом
`Console.Write()`, а затем для получения данных (строки) методом `Console.ReadLine()`. Почему бы это всё не объединить в один метод?

Для этого воспользуемся магией новой версии шаблона `tinytempalte`, но для этого сперва надо удалить старую версию шаблона.

Выполняем последовательно следующие команды:

```
dotnet new uninstall TinyConsoleTemplate.CSharp
dotnet new install TinyConsoleTemplate.CSharp::1.0.9
```
В результате выполнения последней команды вы должны увидеть что-то вроде этого:
```
Планируется установка следующих пакетов шаблонов:
   TinyConsoleTemplate.CSharp::1.0.9

Успешно установлены TinyConsoleTemplate.CSharp::1.0.9 следующие шаблоны:
Имя шаблона            Короткое имя  Язык  Теги
---------------------  ------------  ----  ---------------------
Tiny Console Template  tinyconsole   [C#]  Console/C#/App/Common
```

Теперь, падван, как обычно, создай консольное приложение `ex0076_user_input_bonus` (**с операторами верхнего уровня**)
при помощи шаблона `tinyconsole` в папке `episode02` и добавь его в  файл решения `episode02.sln`. 
Это можно сделать как в командной строке, так и в любой IDE.

В результате, в редакторе IDE, вы должны увидеть следующий код:

```C#
WriteLine("Hello from TinyConsoleTemplate with classic Main method!");
string? name = ReadInput("What is your name? ");
name = string.IsNullOrEmpty(name) ? "Anonymous" : name.Trim();
WriteLine($"Hello, {name}! Enjoy using the TinyConsoleTemplate and the TinyConsoleUtils library to create cool C# console applications!");
```

>Внимание! Среда IDE может в самом начале подчеркнуть метод `ReadInput()` как содержащий ошибку. Это может произойти потому
> что IDE ещё не подтянуло nuget пакет содержащий библиотеку, которая реализует этот метод. Через несколько секунд всё
> уже будет хорошо.
> {style="warning"}

Запустите программу на выполнение и на запрос имени введите своё или другое любое имя. Например:

```
Hello from TinyConsoleTemplate with classic Main method!
What is your name? It0n
Hello, It0n! Enjoy using the TinyConsoleTemplate and the TinyConsoleUtils library to create cool C# console applications!
```

Как видите в коде, теперь вместо двух методов `Console.Write()` и `Console.ReadLine()` для получения пользовательского
ввода мы используем один метод `ReadInput()` в параметрах которого передаем строку запроса информации от пользователя.
В данном случаем мы спрашиваем его имя - **"What is your name? "** и помещаем ответ в переменную `name` типа `string` в
инструкции:

```C#
string? name = ReadInput("What is your name? ");
```

В качестве задания создай приложение `ex0076pt01` с помощью шаблона `tinyconsole`. Приложение для получения данных от 
пользователя должно использовать метод `ReadInput()`. В первом запросе приложение должно спрашивать имя пользователя,
во втором запросе - фамилию пользователя. А затем выводить приветствие, например: "Привет, Вася Пупкин!".

Чтобы было понятнее приведу скриншоты работы приложения:

![Работа приложения ex0076pt01](ex0076pt01result.png){ border-effect="line"  thumbnail="true" width="700" }

На скриншоте видно, что приложение было запущено три раза. Каждый раз вводились разные данные. И соответственно введенным
данным приложение приветствовало пользователя.

Если вы создали приложение из шаблона `tinytemplate` с операторами верхнего уровня, то эта программа у вас должна состоять
всего из трех строк. Этого достаточно для решения данной задачи.

Дерзай, падаван, это легкое задание. Так на разминочку тебе.

В качестве второго задания приложение `ex0076pt02` с помощью шаблона `tinyconsole`. Приложение для получения данных от
пользователя должно использовать метод `ReadInput()`. В первом запросе приложение должно спрашивать первое слагаемое,
во втором - второе слагаемое. И затем выводить сумму введенных чисел. Числа для ввода должны быть целыми числами.
Приложение не должно проверять правильность ввода данных. То есть предполагается что пользователь будет вводить правильные
данные. Обрабатывать ошибки ввода данных не нужно (по скольку вы, пока, не знаете как это делать).

Чтобы было понятнее, приведу скриншот работы приложения:

![Работа приложения ex0076pt02](ex0076pt02result.png){ border-effect="line"  thumbnail="true" width="700" }

Это приложение состоит уже и 5 строк (с учётом одной пустой строки) для отделения инструкции `using System;` от остальной
части кода. То есть по существу из 4 инструкций. Первую из них я уже подсказал.

Дерзай, падван! Это не сложные задания. Всё что тебе нужно для их выполнения ты уже должен знать.