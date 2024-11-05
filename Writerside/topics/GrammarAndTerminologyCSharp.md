# Грамматика и терминология C# 

В обычном языке основной единицей несущей смысловую нагрузку является предложение. Предложение может состоять из одного или более слов.

В большинстве языков конец повествовательного предложения при написании обозначается точкой.

## Инструкции
В C# аналогом предложения можно назвать инструкцию (**statement**), которая заканчивается точкой с запятой. Например:

```c#
Console.WriteLine("Hello, World.");
```
Инструкцию можно рассматривать как предписание компьютеру выполнить определенное действие. В примере выше это вывести в консоль фразу Hello World.

Следовательно, программа - это совокупность инструкций которые выполняют какую-либо задачу.

Давайте рассмотрим простейшую задачу получения от пользователя двух чисел и затем вывода суммы этих чисел.

```c#
using System.Globalization;

namespace ex0010_sum_of_two;

class Program
{
    static void Main(string[] args)
    {
        Console.InputEncoding = System.Text.Encoding.GetEncoding("utf-16");
        Console.Write("Введите первое число: ");
        var input1 = Console.ReadLine();

        Console.Write("Введите второе число: ");
        var input2 = Console.ReadLine();

        // Преобразуем строки в числа с учетом дробной части
        if (double.TryParse(input1, NumberStyles.Any, CultureInfo.InvariantCulture, out double number1) &&
            double.TryParse(input2, NumberStyles.Any, CultureInfo.InvariantCulture, out double number2))
        {
            double sum = number1 + number2;
            Console.WriteLine($"Сумма чисел: {sum}");
        }
        else
        {
            Console.WriteLine("Некорректный ввод. Пожалуйста, введите числа.");
        }

    }
}
```
Создайте папку episode02. Затем в ней создайте проект ex0010_sum_of_two без операторов верхнего уровня. 

![dotnet new console -h](SumOfTowNumbers01.png){ border-effect="line" }

Запустите VSCode из папки episode02, откройте проект ex0010_sum_of_two и введите приведенный выше код в файл Program.cs.
Практика это всегда полезно. Если забыли как это делается, вернитесь к первому эпизоду.

>Если вы запустите VSCode из папки episode02, то VSCode сам создаст файл решения в который добавит проект ex0010_sum_of_two.
{style="note"}

![dotnet new console -h](SumOfTowNumbers03.png){ border-effect="line" }

Запустите программу. Пример запуска:

![dotnet new console -h](SumOfTowNumbers02.png){ border-effect="line" }

Возможно пока этот пример вам не покажется сильно простым, но сложность здесь может представлять только блок преобразования строки в число.
Как раз мы плавно подходим к понятию блоков кода.

Так же в коде вы видите однострочный комментарий поясняющий, что делает блок кода ниже. О комментариях мы тоже поговорим.

Как видите практически каждая строка заканчивается точкой с запятой. Исключением являются только блоки кода, заключенные
в фигурные скобки.

>В документации по C# на сайте Microsoft, а так же в англоязычных книгах используется слово **[statement](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/declarations)**,
>которое я перевел как инструкция. На мой взгляд это правильно отражает смысл слова **statement** в контексте программирования.
>В русскоязычных книгах это слово иногда переводят как выражение, или что ещё хуже как оператор.
{style="note"}

## Комментарии
Комментарии поясняют что делает та или иная часть кода. Комментарии не являются частью программы и игнорируются компилятором.
Если сказать простым языком, то это просто пояснительные заметки которые вы оставляете для себя и других программистов.

Комментарии бывают однострочные и многострочные.

Однострочный комментарий начинается с двух символов косой черты: //. И размещается в одной строке.

Многострочный комментарий начинается с символов /* и закачивается символами */, внутри которых размещается текст комментария.

Давайте посмотрим возможный пример. Добавим в нашу программу ещё комментариев.

```c#
using System.Globalization;

namespace ex0010_sum_of_two // боее явно определили пространство имен
{

    class Program
    {
        static void Main(string[] args)
        {
            Console.InputEncoding = System.Text.Encoding.GetEncoding("utf-16"); // устанавливаем кодировку для символов
            Console.Write("Введите первое число: ");
            var input1 = Console.ReadLine();

            Console.Write("Введите второе число: ");
            var input2 = Console.ReadLine();

            /* 
            Проверяем возможность преобразолвания введенных строк в числа с учетом дробной части.
            И если преобразуется без ошибок, то производится преобразование введенных строк в числа,
            затем вычисляется сумма этих чисел и выводится результат.
            */
            if (double.TryParse(input1, NumberStyles.Any, CultureInfo.InvariantCulture, out double number1) &&
                double.TryParse(input2, NumberStyles.Any, CultureInfo.InvariantCulture, out double number2))
            {
                double sum = number1 + number2; // складываем числа
                Console.WriteLine($"Сумма чисел: {sum}"); // выводим результат
            }
            else
            {   // если введенные данные не удалось преобразовать в числа, то выводим сообщение об ошибке
                Console.WriteLine("Некорректный ввод. Пожалуйста, введите числа.");
            }

        }
    }
}
```
>Разные среды разработки могут иметь различные настройки подсветки комментариев.
> Это можно поменять в настройках среды разработки. 
{style="note"}

Комментарии также можно использовать для исключения из выполнения программы инструкций. Это довольно частый приём используемый
при отладке программ. Например:

```c#
using System.Globalization;

namespace ex0010_sum_of_two // более явно определили пространство имен
{

    class Program
    {
        static void Main(string[] args)
        {
            Console.InputEncoding = System.Text.Encoding.GetEncoding("utf-16"); // устанавливаем кодировку для символов
            Console.Write("Введите первое число: ");
            var input1 = Console.ReadLine(); // здесь получаем строку в переменную input1

            Console.Write("Введите второе число: ");
            var input2 = Console.ReadLine(); // здесь получаем строку в переменную input2

            /* 
            Проверяем возможность преобразолвания введенных строк в числа с учетом дробной части.
            И если преобразуется без ошибок, то производится преобразование введенных строк в числа
            которые заносятся в переменные number1 и nuber2. После чего выводится сумма этих переменных.
            */
            if (double.TryParse(input1, NumberStyles.Any, CultureInfo.InvariantCulture, out double number1) &&
                double.TryParse(input2, NumberStyles.Any, CultureInfo.InvariantCulture, out double number2))
            {
                //double sum = number1 + number2; // закомментировали эту строку, так как в принципе она не нужна для правильной работы программы
                Console.WriteLine($"Сумма чисел: {number1 + number2}"); // выводим результат
            }
            else
            {   // если введенные данные не удалось преобразовать в числа, то выводим сообщение об ошибке
                Console.WriteLine("Некорректный ввод. Пожалуйста, введите числа.");
            }

        }
    }
}
```

Как видите здесь мы закомментировали строку

```c#
double sum = number1 + number2;
```
поставив перед ней две косые черты.

И естественно, чтобы программа работала, чуток изменили код, вычисляя сумму прямо в строке вывода чисел.

>Если вы хорошо проектируете код, используя правильные названия переменных, классов и методов, то такой код, в какой-то
>мере является самодокументируемым. Большое количество комментариев, как правило, свидетельствует об очень плохом коде.
{style="note"}

## Блоки
Блоки кода можно сравнить с абзацами. В C# блоки кода заключаются в фигурные скобки: {}.

Блок начинается с объявления, описывающего то, что мы определяем.
Например, блок может определять пространство имен, класс, метод или оператор, такой как if в нашем случае.

Как я говорил, блоки кода определяются открывающей и закрывающей фигурными скобками: {}. После которых НЕ ставится точка с запятой.

Посмотрите пример ниже. Тут, с помощью комментариев, явно описаны начала и концы блоков кода. Так же вы можете видеть, как
чрезмерные комментарии усложняют чтение кода.

```c#
using System.Globalization;

namespace ex0010_sum_of_two // более явно определили пространство имен
{ // начало блока namespace ex0010_sum_of_two

    class Program
    { // начало блока класса Program
        static void Main(string[] args)
        { // начало блока статического метода Main
            Console.InputEncoding = System.Text.Encoding.GetEncoding("utf-16"); // устанавливаем кодировку для символов
            Console.Write("Введите первое число: ");
            var input1 = Console.ReadLine(); // здесь получаем строку в переменную input1

            Console.Write("Введите второе число: ");
            var input2 = Console.ReadLine(); // здесь получаем строку в переменную input2

            /* 
            Проверяем возможность преобразования введенных строк в числа с учетом дробной части.
            И если преобразуется без ошибок, то производится преобразование введенных строк в числа
            которые заносятся в переменные number1 и nuber2. После чего выводится сумма этих переменных.
            */
            if (double.TryParse(input1, NumberStyles.Any, CultureInfo.InvariantCulture, out double number1) &&
                double.TryParse(input2, NumberStyles.Any, CultureInfo.InvariantCulture, out double number2))
            { // начало блока положительной проверки оператора if
                //double sum = number1 + number2; // закомментировали эту строку, так как в принципе она не нужна для правильной работы программы
                Console.WriteLine($"Сумма чисел: {number1 + number2}"); // выводим результат
            } // конец блока положительной проверки оператора if
            else
            { // начало блока отрицательной проверки оператора if   
                Console.WriteLine("Некорректный ввод. Пожалуйста, введите числа."); // если введенные данные не удалось преобразовать в числа, то выводим сообщение об ошибке
            } // конец блока отрицательной проверки оператора if 

        } // конец блока статического метода Main
    } // конец блока класса Program
} // конец блока namespace ex0010_sum_of_two
```

Среды разработки имеют возможность сворачивать и разворачивать блоки кода, что бывает очень удобно при редактировании
больших файлов, содержащих сотни строк кода. VSCode и JetBrains используют для этого стрелочки смотрящие вниз и в право,
а Visual Studio значки [-] и [+] или так же стрелочки вниз и вправо в зависимости от версии и настроек.
Эти значки появляются кода вы помещаете курсор к левой границе кода где, как правило, находится нумерация строк.

VSCode

![Скрытие и показ блоков кода](CodeBlocks01.png){ border-effect="line"  thumbnail="true" width="700" }

JetBrains Rider

![Скрытие и показ блоков кода](CodeBlocks02.png){ border-effect="line"  thumbnail="true" width="700" }

Visual Studio 2022

![Скрытие и показ блоков кода](CodeBlocks03.png){ border-effect="line"  thumbnail="true" width="700" }

## Регионы

Регионы позволяют вам самим определить куски кода которые вы можете сворачивать как блоки. 

Для определения начала региона используется ключевое слово `#region`, для определения конца региона - ключевой слово `#endregion`.

Давайте уберем все комментарии из нашего кода и определим блок кода, который хотим сворачивать и разворачивать.

![Определение региона кода](Region01.png){ border-effect="line"  thumbnail="true" width="700" }

Добавили регион и появилась возможность свернуть указанный кусок кода.

![Сворачивание региона](Region02.png){ border-effect="line"  thumbnail="true" width="700" }

Свернём регион.

![Сворачивание региона](Region03.png){ border-effect="line"  thumbnail="true" width="700" }

Как видите после ключевого слова `#region` так же можно использовать комментарий для описания региона.

## Ключевые слова

В C# можно выделить два вида ключевых слов:
- [ключевые слова](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/) ([keywords](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/))
- [контекстные ключевые слова](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/#contextual-keywords) ([contextual keywords](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/#contextual-keywords))

**Ключевые слова C#** — это специальные зарезервированные слова, которые используются для обозначения основных конструкций 
и команд в языке программирования C#. Они являются частью самого языка и имеют особое значение. Например, такие слова, 
как `int`, `class`, `if`, `for`, `return`, `public` — это ключевые слова. Они необходимы для написания кода и создания 
структур, таких как классы, методы, условия, циклы и многое другое.

**Контекстные ключевые слова C#** — это слова, которые действуют как ключевые только в определённых ситуациях (контексте), 
где они имеют специальное значение. В других случаях их можно использовать как обычные имена переменных или других элементов. 
Примеры контекстных ключевых слов: `add`, `get`, `partial`, `value`. Например, слово `partial` является контекстным 
ключевым словом, которое обозначает частичный класс, но его можно использовать как имя переменной или метода в другом контексте.

### В чем разница?
1. **Ключевые слова** всегда зарезервированы, и их нельзя использовать как имена переменных, методов или классов. Если попытаться использовать их в таком качестве, произойдет ошибка.

   Пример:
   ```c#
   int int = 5; // Ошибка, так как `int` — ключевое слово
   ```

2. **Контекстные ключевые слова** можно использовать как обычные слова, если они не находятся в специальном контексте. Например, `partial` вне контекста классов и методов не имеет специального значения.

   Пример:
   ```c#
   public partial class MyClass { }  // Здесь `partial` — ключевое слово для определения частичного класса
   
   int partial = 5;  // Здесь `partial` можно использовать как имя переменной, потому что это не специальный контекст
   ```

Ниже приведены таблицы со всеми ключевыми словами и контекстными ключевыми словами C#. Не пугайтесь их количеству. 
Уверяю вас вы всё это запомните автоматически в процессе изучения языка. Пока для ознакомления просто пробегитесь по этим 
таблицам. Так сказать чтобы отложилось на подкорочку. Скорее всего, пока, вам многое из этих таблиц будет не понятно.
Но это пока. Терпенье и труд все перетрут :)

Можете воспринимать этот раздел как справочную структурированную информацию по ключевым словам C#. Заучивать всё это нет
ни какой необходимости. Как я уже говорил, вы автоматически всё это запомните в процессе обучения.

В принципе, в какой-то мере, прогресс в **начальном изучении** C# можно измерять по количеству изученных ключевых слов и их
применению на практике. Хотя, конечно же, простого изучения ключевых слов не достаточно для полного владения C#.

Это можно сравнить с изучением обычного иностранного языка. Безусловно вы должны знать иностранные слова. Помните карточки
для заучивания слов, их звучания и перевода? Но одного знания слов не достаточно для владения языком. Можно знать много 
иностранных слов, но не уметь общаться на этом языке. Словарный запас это основа. А вот складывание слов в правильно
грамматически построенные предложения это уже и есть искусство владение языком.

Кроме того в каждом языке есть устойчивые выражения, которые нужно знать. Их можно сравнить с паттернами или лучшими 
практиками в программировании.

### Таблица 1: Ключевые слова C#

| Ключевое слово | Описание | Ссылка на документацию |
|----------------|----------|------------------------|
| `abstract`     | Определяет абстрактный класс или метод, который должен быть реализован в производных классах. | [abstract](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/abstract) |
| `as`           | Приводит объект к указанному типу, если возможно; возвращает `null` при неудаче. | [as](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/as) |
| `base`         | Ссылается на базовый класс текущего экземпляра. | [base](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/base) |
| `bool`         | Определяет логический тип данных (`true` или `false`). | [bool](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/bool) |
| `break`        | Завершает выполнение цикла или оператора `switch`. | [break](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/break) |
| `byte`         | Представляет целое число без знака от 0 до 255. | [byte](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/byte) |
| `case`         | Определяет блок кода в `switch`, выполняемый при совпадении значения. | [case](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/switch) |
| `catch`        | Обрабатывает исключения, возникшие в блоке `try`. | [catch](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/try-catch) |
| `char`         | Представляет символьный тип. | [char](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/char) |
| `checked`      | Контролирует переполнение арифметических операций. | [checked](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/checked) |
| `class`        | Определяет класс. | [class](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/class) |
| `const`        | Определяет константу, значение которой не изменяется после инициализации. | [const](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/const) |
| `continue`     | Переходит к следующей итерации цикла. | [continue](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/continue) |
| `decimal`      | Представляет десятичный тип с плавающей запятой для финансовых вычислений. | [decimal](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/decimal) |
| `default`      | Указывает значение по умолчанию для типа или `case` в `switch`. | [default](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/default) |
| `delegate`     | Определяет делегат — ссылку на метод. | [delegate](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/delegate) |
| `do`           | Создает цикл, который выполняется хотя бы один раз, даже если условие ложно. | [do](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/do) |
| `double`       | Представляет число с плавающей запятой двойной точности. | [double](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/double) |
| `else`         | Определяет альтернативный блок кода для выполнения, если условие `if` ложно. | [else](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/if-else) |
| `enum`         | Объявляет перечисление — набор именованных констант. | [enum](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/enum) |
| `event`        | Объявляет событие, уведомляющее подписчиков о происходящих действиях. | [event](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/event) |
| `explicit`     | Определяет явное преобразование типа. | [explicit](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/explicit) |
| `extern`       | Указывает, что метод реализован вне текущей сборки. | [extern](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/extern) |
| `false`        | Представляет логическое значение `false`. | [false](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/false) |
| `finally`      | Определяет блок кода, который выполняется независимо от того, произошла ли ошибка в `try`. | [finally](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/finally) |
| `fixed`        | Закрепляет указатель на объект в управляемой куче. | [fixed](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/fixed) |
| `float`        | Представляет число с плавающей запятой одинарной точности. | [float](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/float) |
| `for`          | Создает цикл с параметрами инициализации, условия и итерации. | [for](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/for) |
| `foreach`      | Итерация по элементам коллекции. | [foreach](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/foreach-in) |
| `goto`         | Переносит управление к определенной метке. | [goto](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/goto) |
| `if`           | Определяет условие для выполнения блока кода. | [if](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/if-else) |
| `implicit`     | Определяет неявное преобразование типа. | [implicit](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/implicit) |
| `in`           | Используется для передачи параметра по ссылке без изменения его значения. | [in](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/in-parameter-modifier) |
| `int`          | Представляет целое число со знаком от -2,147,483,648 до 2,147,483,647. | [int](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/int) |
| `interface`    | Определяет контракт, который должны реализовать классы. | [interface](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/interface) |
| `internal`     | Ограничивает видимость элементов в пределах одной сборки. | [internal](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/internal) |
| `is`           | Проверяет, является ли объект указанным типом. | [is](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/is) |
| `lock`         | Ограничивает доступ к разделяемому ресурсу в многопоточной среде. | [lock](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/lock) |
| `long`         | Представляет целое число со знаком от -9,223,372,036,854,775,808 до 9,223,372,036,854,775,807. | [long](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/long) |
| `namespace`    | Организует классы и другие типы в пространства имен. | [namespace](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/namespace) |
| `new`          | Создает экземпляр объекта или скрывает наследованный член. | [new](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/new) |
| `null`         | Представляет отсутствие значения. | [null](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/null) |
| `object`       | Базовый тип для всех типов C#. | [object](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/object) |
| `operator`     | Определяет оператор для пользовательских типов. | [operator](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/operator) |
| `out`          | Используется для передачи параметра по ссылке, позволяя изменять его значение. | [out](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/out-parameter-modifier) |
| `override`     | Переопределяет виртуальный метод базового класса. | [override](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/override) |
| `params`       | Позволяет передавать переменное число аргументов в метод. | [params](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/params) |
| `private`      | Ограничивает видимость элементов внутри класса или структуры. | [private](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/private) |
| `protected`    | Ограничивает видимость элементов внутри класса и его производных. | [protected](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/protected) |
| `public`       | Определяет общедоступные элементы. | [public](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/public) |
| `readonly`     | Определяет поле, значение которого можно установить только при инициализации или в конструкторе. | [readonly](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/readonly) |
| `ref`          | Передает параметр по ссылке. | [ref](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/ref) |
| `return`       | Завершает выполнение метода и возвращает значение (если метод не `void`). | [return](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/return) |
| `sbyte`        | Представляет целое число со знаком от -128 до 127. | [sbyte](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/sbyte) |
| `sealed`       | Запрещает наследование от класса. | [sealed](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/sealed) |
| `short`        | Представляет целое число со знаком от -32,768 до 32,767. | [short](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/short) |
| `sizeof`       | Возвращает размер типа в байтах. | [sizeof](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/sizeof) |
| `stackalloc`   | Выделяет массив в стеке. | [stackalloc](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/stackalloc) |
| `static`       | Указывает, что элемент принадлежит типу, а не экземпляру. | [static](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/static) |
| `string`       | Представляет строку. | [string](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/string) |
| `struct`       | Определяет значение типа структуры. | [struct](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/struct) |
| `switch`       | Выбирает блок для выполнения на основе значения. | [switch](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/switch) |
| `this`         | Ссылается на текущий экземпляр класса. | [this](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/this) |
| `throw`        | Вызывает исключение. | [throw](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/throw) |
| `true`         | Представляет логическое значение `true`. | [true](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/true) |
| `try`          | Определяет блок кода для обработки исключений. | [try](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/try-catch) |
| `typeof`       | Возвращает тип объекта. | [typeof](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/typeof) |
| `uint`         | Представляет целое число без знака от 0 до 4,294,967,295. | [uint](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/uint) |
| `ulong`        | Представляет целое число без знака от 0 до 18,446,744,073,709,551,615. | [ulong](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/ulong) |
| `unchecked`    | Игнорирует проверку переполнения арифметических операций. | [unchecked](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/unchecked) |
| `unsafe`       | Позволяет использовать небезопасный код. | [unsafe](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/unsafe) |
| `ushort`       | Представляет целое число без знака от 0 до 65,535. | [ushort](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/ushort) |
| `using`        | Объявляет пространство имен или определяет контекст с автоматическим освобождением ресурсов. | [using](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/using) |
| `virtual`      | Указывает, что метод может быть переопределен в производных классах. | [virtual](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/virtual) |
| `void`         | Указывает, что метод не возвращает значения. | [void](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/void) |
| `volatile`     | Указывает, что значение переменной может изменяться в любой момент. | [volatile](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/volatile) |
| `while`        | Создает цикл, который выполняется до тех пор, пока условие истинно. | [while](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/while) |

### Таблица 2: Контекстные ключевые слова C#

Вот таблица со всеми контекстными ключевыми словами C#, их описаниями и ссылками на документацию на сайте Microsoft:

| Контекстное ключевое слово | Описание                                                                                 | Ссылка на документацию                                                                                                  |
|----------------------------|------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| `add`                      | Добавляет обработчик события.                                                            | [add](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/add)                                       |
| `alias`                    | Создает псевдоним для имени пространства имен или типа.                                  | [extern alias](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/extern)                           |
| `ascending`                | Указывает сортировку по возрастанию в LINQ-запросах.                                     | [ascending](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/ascending)                           |
| `async`                    | Указывает, что метод, лямбда-выражение или анонимная функция выполняется асинхронно.     | [async](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/async)                                   |
| `await`                    | Приостанавливает выполнение метода до завершения асинхронной операции.                   | [await](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/await)                                   |
| `by`                       | Используется в выражениях `group` и `orderby` для указания критерия группировки или сортировки. | [by](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/by) |
| `descending`               | Указывает сортировку по убыванию в LINQ-запросах.                                        | [descending](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/descending)                         |
| `dynamic`                  | Определяет тип данных, который проверяется во время выполнения, а не компиляции.        | [dynamic](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/dynamic)                               |
| `equals`                   | Используется в выражениях `join` для определения условия соединения.                     | [equals](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/equals)                                 |
| `from`                     | Используется в LINQ-запросах для указания источника данных.                              | [from](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/from-clause)                              |
| `get`                      | Определяет аксессор для получения значения свойства или индексатора.                     | [get](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/get)                                       |
| `global`                   | Ссылается на глобальное пространство имен.                                               | [global](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/global)                                 |
| `group`                    | Группирует результаты в LINQ-запросах.                                                   | [group](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/group)                                   |
| `init`                     | Определяет аксессор для инициализации свойства только во время создания объекта.        | [init](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/init)                                     |
| `into`                     | Используется в LINQ-запросах для продолжения запроса после оператора `group` или `select`. | [into](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/into)                                 |
| `join`                     | Выполняет соединение двух последовательностей в LINQ-запросах.                           | [join](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/join-clause)                              |
| `let`                      | Создает промежуточное значение в LINQ-запросах.                                          | [let](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/let)                                       |
| `nameof`                   | Получает строку с именем указанного символа (например, переменной, типа или члена).      | [nameof](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/nameof)                                 |
| `notnull`                  | Задает ограничение универсального параметра, позволяя использовать только ненулевые типы. | [notnull](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/notnull-constraint)                   |
| `on`                       | Используется в выражениях `join` для определения условия соединения в LINQ-запросах.     | [on](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/on)                                         |
| `orderby`                  | Сортирует результаты в LINQ-запросах.                                                    | [orderby](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/orderby)                               |
| `partial`                  | Позволяет определить частичный класс, структуру, интерфейс или метод.                    | [partial](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/partial-type)                          |
| `record`                   | Определяет неизменяемый тип записи.                                                      | [record](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/record)                                 |
| `remove`                   | Удаляет обработчик события.                                                              | [remove](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/remove)                                 |
| `select`                   | Используется в LINQ-запросах для проекции каждого элемента в новую форму.                | [select](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/select)                                 |
| `set`                      | Определяет аксессор для задания значения свойства или индексатора.                       | [set](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/set)                                       |
| `unmanaged`                | Ограничивает универсальный параметр типами, поддерживающими указатели.                   | [unmanaged](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/unmanaged-constraint)               |
| `value`                    | Представляет значение свойства или индексатора в аксессоре `set`.                        | [value](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/value)                                   |
| `var`                      | Позволяет компилятору автоматически выводить тип переменной на основе присваиваемого значения. | [var](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/var)                                   |
| `when`                     | Определяет условие для фильтрации в `catch` и `case`.                                    | [when](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/when)                                     |
| `where`                    | Задает ограничения для параметров типа или фильтрует результаты LINQ-запросов.           | [where](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/where-clause)                            |
| `with`                     | Позволяет копировать объект с изменением некоторых свойств в выражениях с записями.      | [with](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/with)                                     |
| `yield`                    | Используется для возвращения значений по одному в методах, которые возвращают `IEnumerable`. | [yield](https://learn.microsoft.com/dotnet/csharp/language-reference/keywords/yield)                               |

## Категории ключевых слов
Чтобы лучше запомнить, а главное понять области применения ключевых слов, все их можно разделить на категории и подкатегории.

- [Модификаторы (Modifiers)](#Modifiers)
    - [Модификаторы доступа (Access Modifiers)](#AccessModifiers)
- [Ключевые слова инструкций (Statement keywords)](#StatementKeywords)


Опять же, всё это вы запомните автоматически в процессе изучения. Этот раздел тоже относится к справочной информации к 
которой вы можете вернуться в любой момент.

Сперва просто пробегитесь по этой информации, чтобы получить общее представление. Скорее всего, если вы только начали изучать
C#, многое для вас будет не понятно, но это не страшно. На подкорочке осядет и всегда можете вернуться и почитать ещё раз.

### Ключевые слова модификаторы {id="Modifiers"}

**Ключевые слова-модификаторы** в C# — это ключевые слова, используемые для задания дополнительных характеристик типов и их членов. 
Они определяют, как и где можно использовать и изменять типы, методы, поля, свойства и другие члены. Модификаторы 
управляют уровнями доступа, возможностью наследования, статическим или экземплярным поведением, а также другими аспектами.

1. **`public`** — Общедоступный, доступен везде.
2. **`private`** — Доступен только внутри содержащего типа.
3. **`protected`** — Доступен внутри содержащего класса и его производных классов.
4. **`internal`** — Доступен только в пределах текущей сборки.
5. **`protected internal`** — Доступен в пределах текущей сборки или производных классов.
6. **`private protected`** — Доступен в пределах содержащего класса и его производных классов, но только в текущей сборке.
7. **`static`** — Указывает, что член или тип является статическим и принадлежит типу, а не экземпляру.
8. **`readonly`** — Поле, значение которого можно задать только при инициализации или в конструкторе.
9. **`const`** — Указывает, что значение поля является константным и задается во время компиляции.
10. **`virtual`** — Метод, который может быть переопределен в производном классе.
11. **`abstract`** — Указывает, что класс или член является абстрактным и должен быть реализован в производном классе.
12. **`sealed`** — Запрещает наследование от класса или переопределение метода.
13. **`override`** — Переопределяет виртуальный метод или метод интерфейса в производном классе.
14. **`async`** — Позволяет использовать `await` в методе для асинхронного выполнения.
15. **`unsafe`** — Позволяет использовать небезопасный код, например указатели.
16. **`extern`** — Указывает, что метод реализован вне текущего кода (например, в библиотеке).
17. **`volatile`** — Указывает, что значение поля может быть изменено одновременно в разных потоках.
18. **`new`** — Скрывает члены с тем же именем, унаследованные от базового класса.
19. **`partial`** — Позволяет разбивать реализацию класса, интерфейса или метода на несколько файлов.
20. **`file`** — Ограничивает видимость типа текущим исходным файлом (начиная с C# 11).
21. **`event`** — Используется для объявления событий, которые могут подписывать и обрабатывать другие части кода. Определяет событие, доступное для подписчиков.
22. **`in`** (generic modifier) — Ограничивает параметр типа как входной (ковариантный), что позволяет использовать более общий тип вместо конкретного.
23. **`out`** (generic modifier) — Ограничивает параметр типа как выходной (контравариантный), что позволяет использовать более специфический тип вместо общего.

Эти модификаторы помогают контролировать видимость, использование, передачу и изменение данных,
а так же применяются для управления структурой и поведением кода, делая типы более гибкими и управляемыми.

Из этого большого списка ключевых слов модификаторов обычно выделяют группу модификаторов доступа.

**[Модификаторы доступа](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/access-modifiers) ([Access Modifiers](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/access-modifiers))** {id="AccessModifiers"}

Выделим в отдельный список ключевые слова модификаторы доступа:

1. **`public`** — Доступен из любого кода в пределах программы или другой сборки.
2. **`protected`** — Доступен только из содержащего класса и его производных классов.
3. **`internal`** — Доступен только внутри текущей сборки.
4. **`private`** — Доступен только в пределах содержащего типа.
5. **`file`** — Доступен только в пределах текущего исходного файла (добавлен в C# 11).

С помощью этих пяти модификаторов доступа, можно определить семь уровней доступности

**[Уровни доступности](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/accessibility-levels) ([Accessibility Levels](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/accessibility-levels))**

1. **`public`** — Доступ не ограничен.
2. **`protected`** — Доступ ограничен содержащим классом или типами, производными от содержащего класса.
3. **`internal`** — Доступ ограничен текущей сборкой.
4. **`protected internal`** — Доступ ограничен текущей сборкой или типами, производными от содержащего класса.
5. **`private`** — Доступ ограничен содержащим типом.
6. **`private protected`** — Доступ ограничен содержащим классом или типами, производными от содержащего класса, внутри текущей сборки.
7. **`file`** — Объявленный тип виден только в текущем исходном файле. Типы, ограниченные файлом, обычно используются для генераторов исходного кода.

Эти модификаторы доступа и определяемые ими уровни доступности помогают контролировать видимость и доступ к типам и их членам в коде,
что позволяет лучше управлять доступом и защищать данные от ненужного доступа.

Уровни доступности определяют [область доступности](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/accessibility-domain) ([accessibility domain](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/accessibility-domain)) 
члена представляющую собой реальный "диапазон", от куда к нему можно обращаться. 
Она зависит не только от его уровня доступа, но и от того, где он объявлен в коде. Область доступности определяется следующими факторами:
- **Местоположение члена** (например, внутри класса, структуры или интерфейса).
- **Уровень доступа** (например, `private`, `public`, и т.д.).

Таким образом, область доступности накладывает дополнительные ограничения, исходя из места объявления члена или типа.

Уровни доступности задают общее правило, а область доступности применяет это правило, учитывая расположение члена или типа в программе.

Например:

- **Члены с `private` уровнем доступа**: их область доступности ограничивается только тем классом или типом, в котором они объявлены.
- **Члены с `internal` уровнем доступа**: их областью доступности является весь проект или сборка, так как доступ к ним ограничен этой сборкой.
- **Вложенные типы**: их область доступности не выходит за пределы их внешнего типа. Например, если вложенный тип объявлен как `private` внутри другого класса, он доступен только внутри этого класса, даже если внешний класс — `public`.

***Примеры***

1. **`private` член класса**:
   ```c#
   public class OuterClass
   {
       private int privateField; // Доступ только в пределах OuterClass

       public void Method()
       {
           Console.WriteLine(privateField); // Доступно, так как вызывается внутри OuterClass
       }
   }
   ```

   `privateField` имеет `private` уровень доступа, поэтому его область доступности ограничена классом `OuterClass`, несмотря на то, что `OuterClass` — `public`.

2. **`internal` класс в проекте**:
   ```c#
   internal class InternalClass // Доступен только в текущей сборке
   {
       public void Greet()
       {
           Console.WriteLine("Hello from InternalClass");
       }
   }
   ```

   `InternalClass` имеет `internal` уровень доступа, и его область доступности охватывает всю текущую сборку, но не выходит за её пределы.

Уровень доступности устанавливает "потенциальную" видимость типа или члена, в то время как область доступности уточняет, 
где именно в программе он реально доступен, учитывая место его объявления и уровень доступа.

**[Ограничения на использование уровней доступности](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/restrictions-on-using-accessibility-levels) ([Restrictions on using accessibility levels](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/restrictions-on-using-accessibility-levels))**

| Контекст                    | Ограничение                                                                                                                                                                                                                                                |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Типы верхнего уровня**    | У типов верхнего уровня может быть только `public` или `internal` доступ. Типы верхнего уровня не могут быть `private`, `protected`, `protected internal`, или `private protected`.                                                                        |
| **Пространства имен**       | Пространства имен не могут иметь уровней доступа. Модификаторы доступа не применимы к пространствам имен.                                                                                                                                                  |
| **Классы**                  | Прямой базовый класс для типа класса должен иметь по крайней мере такой же уровень доступности, как и сам тип класса.                                                                                                                                      |
| **Интерфейсы**              | Явные базовые интерфейсы для типа интерфейса должны иметь по крайней мере такой же уровень доступности, как и сам тип интерфейса.                                                                                                                          |
| **Делегаты**                | Тип возвращаемого значения и типы параметров для типа делегата должны иметь по крайней мере такой же уровень доступности, как и сам тип делегата.                                                                                                          |
| **Константы**               | Тип константы должен иметь по крайней мере такой же уровень доступности, как и сама константа.                                                                                                                                                             |
| **Поля**                    | Тип поля должен иметь по крайней мере такой же уровень доступности, как и само поле.                                                                                                                                                                       |
| **Методы**                  | Тип возвращаемого значения и типы параметров для метода должны иметь по крайней мере такой же уровень доступности, как и сам метод.                                                                                                                        |
| **Свойства**                | Тип свойства должен иметь по крайней мере такой же уровень доступности, как и само свойство.                                                                                                                                                               |
| **События**                 | Тип события должен иметь по крайней мере такой же уровень доступности, как и само событие.                                                                                                                                                                 |
| **Индексаторы**             | Тип и типы параметров для индексатора должны иметь по крайней мере такой же уровень доступности, как и сам индексатор.                                                                                                                                     |
| **Операторы**               | Тип возвращаемого значения и типы параметров для оператора должны иметь по крайней мере такой же уровень доступности, как и сам оператор.                                                                                                                  |
| **Конструкторы**            | Типы параметров для конструктора должны иметь по крайней мере такой же уровень доступности, как и сам конструктор.                                                                                                                                         |
| **Переопределение методов** | Переопределенный метод (`override`) не может иметь уровень доступа ниже, чем у метода в базовом классе.                                                                                                                                                    |
| **Реализация интерфейсов**  | Метод, реализующий интерфейс, должен быть `public`. Другие уровни доступа недопустимы.                                                                                                                                                                     |
| **Вложенные типы**          | Уровень доступа вложенного типа не может быть шире, чем у содержащего его типа.                                                                                                                                                                            |
| **protected internal и private protected** | `protected internal` доступен внутри сборки и в производных классах из других сборок. `private protected` доступен только в текущей сборке и только для производных классов. Эти модификаторы нельзя использовать для интерфейсов и типов верхнего уровня. |
| **Конструкторы структур**   | Конструкторы структур не могут быть `protected`, `protected internal`, или `private protected`.                                                                                                                                                            |

Если модификатор доступа не указывается в объявлении члена, используется доступность по умолчанию.

| Члены типа    | Уровень доступности по умолчанию | Допустимые объявленные уровни доступности                                                                 |
|---------------|----------------------------------|----------------------------------------------------------------------------------------------------------|
| **enum**      | public                           | Невозможно задать другие уровни доступности                                                              |
| **class**     | private                          | public, protected, internal, private, protected internal, private protected                              |
| **interface** | public                           | public, protected, internal, private* (при наличии реализации по умолчанию), protected internal, private protected |
| **struct**    | private                          | public, internal, private                                                                               |

***Примечания***
- **enum** всегда имеет уровень доступа `public` и не может быть объявлен с другими уровнями.
- **class** имеет `private` доступ по умолчанию, если вложен в другой тип, и может иметь любые уровни доступа.
- **interface** имеет `public` доступ по умолчанию. Можно указать `private` для методов, если они содержат реализацию по умолчанию.
- **struct** имеет `private` доступ по умолчанию, если вложен в другой тип, и допускает уровни `public`, `internal`, и `private`.

> \*Члены интерфейса с модификатором `private` должны включать реализацию по умолчанию, что позволяет ограничить их доступ исключительно для использования внутри интерфейса.

### Ключевые слова инструкций (Statement keywords) {id="StatementKeywords"}
Как я говорил слово **statement** часто переводят как оператор. Поэтому, данный раздел мог бы называться ключевые
слова операторов, но на мой взгляд такой перевод слова **statement** в контексте программирования на C# не корректен.
Хотя автоматический переводчик на сайте документации Microsoft тоже переводит слово **statement** как оператор.

Давайте посмотрим как на английском выглядят разделы документации на сайте Microsoft:

![ИструкцииОператоры](StatementsAndOperators.png){ border-effect="line"  thumbnail="true" width="700" }

И как эти же разделы выглядят на русском:

![ИструкцииОператоры](StatementsAndOperatorsRus.png){ border-effect="line"  thumbnail="true" width="700" }

Как видите такой перевод только вносит путаницу в понимание сразу нескольких тем. Имейте это в виду.

Но это было так, лирическое отступление от темы связанное с трудностями перевода которые встречаются в русской литературе и
документации.

В C# [ключевые слова инструкций](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/statement-keywords) ([statement keywords](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/statement-keywords)) 
— это команды, которые управляют выполнением программы. 
Они позволяют ветвить, выполнять циклы, обрабатывать ошибки, управлять памятью и синхронизацией и т.д.

| Категория инструкции                                                                                                                                                     | Ключевые слова                                               |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| [Условные инструкции](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/selection-statements)                        | `if`, `switch`                                               |
| [Циклические инструкции](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/iteration-statements)                    | `do`, `for`, `foreach`, `while`                              |
| [Инструкции перехода](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/jump-statements)                             | `break`, `continue`, `goto`, `return`                        |
| [Инструкции обработки исключений](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/exception-handling-statements) | `throw`, `try-catch`, `try-finally`, `try-catch-finally`     |
| [Инструкции контроля переполнения](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/checked-and-unchecked-statements) | `checked`, `unchecked`                                       |
| [Фиксированные инструкции](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/fixed-statement)                       | `fixed`                                                      |
| [Инструкция блокировки](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/lock-statement)                           | `lock`                                                       |
| [Инструкция yield](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/yield-statement)                                | `yield`                                                      |

