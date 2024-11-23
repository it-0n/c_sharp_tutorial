# Элементы языка C#

>Это самая нудная и скучная глава в курсе. По крайней мере я на это сильно надеюсь. Здесь всего парочка практических упражнений.
> Вы можете рассматривать эту главу как очень краткий справочник по языку. Кроме того эта глава позволит вам в голове 
> создать структурированное представление об элементах языка C#. Скорее всего многое из написанного тут вам будет не особо понятно,
> тем более если вы только начинаете изучать C#. Не переживайте по этому поводу. Просто прочитайте это. Всё равно на подкорочке осядет 😊
> И ещё одна польза от этого чтива это то что вы будете разбираться в терминологии и понятиях языка C#.
{style="note"}

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

![Структура каталогов](SumOfTowNumbers01.png){ border-effect="line" }

Запустите VSCode из папки episode02, откройте проект ex0010_sum_of_two и введите приведенный выше код в файл Program.cs.
Практика это всегда полезно. Если забыли как это делается, вернитесь к первому эпизоду.

>Если вы запустите VSCode из папки episode02, то VSCode сам создаст файл решения в который добавит проект ex0010_sum_of_two.
{style="note"}

![Файл решения](SumOfTowNumbers03.png){ border-effect="line" }

Запустите программу. Пример запуска:

![Результат работы программы](SumOfTowNumbers02.png){ border-effect="line" }

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
Но это пока. Терпенье и труд все перетрут 😊

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
Чтобы лучше запомнить, а главное понять области применения ключевых слов, все их можно разделить на категории и подкатегории:

- [Ключевые слова типов](#TypeKeywords)
- [Модификаторы (Modifiers)](#Modifiers)
   - [Модификаторы доступа (Access Modifiers)](#AccessModifiers)
- [Ключевые слова инструкций (Statement keywords)](#StatementKeywords)
- [Параметры методов (Method Parameters)](#MethodParameters)
- [Ключевые слова пространства имён (Namespace keywords)](#NamespaceKeywords)
- [Ключевые слова ограничения обобщений (Generic type constraint keywords)](#GenericTypeConstraintKeywords)
- [Ключевые слова доступа (Access keywords)](#AccessKeywords)
- [Ключевые слова литералы (Literal keywords)](#LiteralKeywords)
- [Контекстные ключевые слова (Contextual Keywords)](#ContextualKeywords)
- [Ключевые слова запросов (Query keywords)](#QueryKeywords)

Опять же, всё это вы запомните автоматически в процессе изучения. Этот раздел тоже относится к справочной информации к
которой вы можете вернуться в любой момент.

Сперва просто пробегитесь по этой информации, чтобы получить общее представление. Скорее всего, если вы только начали изучать
C#, многое для вас будет не понятно, но это не страшно. На подкорочке осядет и всегда можете вернуться и почитать ещё раз.

### Ключевые слова типов {id=TypeKeywords}
Для меня тайна почему на сайте документации Microsoft эти ключевые слова не были выделены в отельную категорию и вообще не 
упомянуты в разделе ключевых слов, но мы исправим это упущение.

**Ключевые слова [типов значений](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-types)**
- **[Целочисленные типы](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/integral-numeric-types):** `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`
- **[Числовые типы с плавающей запятой](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types):** `float`, `double`, `decimal`
- **[Логический тип](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/bool):** `bool`
- **[Символьный тип](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/char):** `char`
- **[Нативные целые типы](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/integral-numeric-types#native-sized-integers):** `nint`, `nuint` (зависят от платформы)
- **[Структуры](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/integral-numeric-types#native-sized-integers):** `struct`
- **[Перечисления](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/enum):** `enum`

**Ключевые слова [ссылочных типов](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/reference-types)**
- **[Классы](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/class):** `class`
- **[Интерфейсы](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/interface):** `interface`
- **[Записи](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/record):** `record`
- **[Встроенные ссылочные типы](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/reference-types):**
   - **`object`** — [базовый тип для всех объектов](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/reference-types#the-object-type)
   - **`string`** — [строковый тип](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/reference-types#the-string-type)
   - **`dynamic`** — [тип, определяемый во время выполнения](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/reference-types#the-dynamic-type)
   - **`delegate`** - [делегаты](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/reference-types#the-delegate-type)

### Модификаторы (Modifiers) {id=Modifiers}
**Модификаторы** в C# — это ключевые слова, используемые для задания дополнительных характеристик типов и их членов. 
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
24. **`global`** — Задает глобальную область видимости для `using` директивы. Появился в C#10.

Эти модификаторы помогают контролировать видимость, использование, передачу и изменение данных,
а так же применяются для управления структурой и поведением кода, делая типы более гибкими и управляемыми.

Из этого большого списка ключевых слов модификаторов обычно выделяют группу модификаторов доступа.

**[Модификаторы доступа](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/access-modifiers) ([Access Modifiers](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/access-modifiers))** {id=AccessModifiers}

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

### Ключевые слова инструкций (Statement keywords) {id=StatementKeywords}
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

### Параметры методов (Method Parameters) {id=MethodParameters}

В C# существует несколько ключевых слов для [параметров методов](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/method-parameters) ([Method Parameters](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/method-parameters)):

1. **`in`**:
   - Передаёт аргумент по ссылке, защищая его от изменений.
   - Может быть временно скопирован, что позволяет использовать его с выражениями или константами.
   - Идеален для больших структур, предотвращая лишние копии.

2. **`ref`**:
   - Позволяет передавать аргумент по ссылке с возможностью его изменения внутри метода.
   - Используется, когда нужно изменять данные.

3. **`out`**:
   - Параметр, который должен быть инициализирован внутри метода.
   - Применяется для возврата нескольких значений из метода.

4. **`params`**:
   - Позволяет передавать переменное количество аргументов в метод.
   - Используется для создания методов, принимающих массив аргументов.

5. **`ref readonly`**:
   - Передаёт аргумент по ссылке для чтения, защищая его от изменений.
   - Не допускает создание временной копии, обеспечивая высокую производительность при работе с большими значениями.

### Ключевые слова пространства имён (Namespace keywords) {id=NamespaceKeywords}

В языке C# для работы с пространствами имен используются несколько ключевых слов:

1. **[namespace](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/namespace)** — определяет область, содержащую связанные классы и другие типы. Структура `namespace` помогает организовывать код и предотвращает конфликты имен.

2. **[using](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/using-directive)** — упрощает доступ к пространствам имен и их содержимому в файле кода. Также может использоваться с модификаторами `global` и `static`.

3. **[global](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/using-directive#global-modifier)** — задает глобальную область видимости для `using` директивы. Появился в C#10.

4. **[static](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/using-directive#static-modifier)** — импортирует статические члены класса, доступные без указания имени класса.

5. **[extern](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/extern-alias)** — поддерживает использование разных версий библиотек с одинаковыми именами пространств.

### Ключевые слова ограничения обобщений (Generic type constraint keywords) {id=GenericTypeConstraintKeywords}

В C# для ограничения обобщенных типов используются два ключевых слова:

1. **[where](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/where-generic-type-constraint)** — ограничивает параметры обобщений, задавая условия на тип. Например, `where T : class` ограничивает тип `T` классами, а `where T : struct` — только структурами. Можно также указать интерфейсы и другие классы, чтобы ограничить типы.

2. **[new](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/new-constraint)** — требует наличия публичного конструктора без параметров у типа `T`. Например, `where T : new()` позволит создавать экземпляры типа `T` в методе, используя `new T()`.

Эти ограничения помогают контролировать, какие типы можно использовать с обобщениями.

### Ключевые слова доступа (Access keywords) {id=AccessKeywords}
В C# ключевые слова **`this`** и **`base`** помогают работать с объектами и иерархией классов:

1. **[this](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/)** используется для ссылки на текущий экземпляр класса. Оно позволяет:
    - Указывать член класса, если он скрыт параметром с тем же именем.
    - Передавать текущий объект в другие методы или для индексации.
    - Используется в методах расширения, где обозначает параметр-экземпляр.

2. **[base](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/base)** используется для обращения к членам базового класса. Используется для:
    - Вызова метода или конструктора из базового класса, часто при переопределении методов в производном классе.

### Ключевые слова литералы (Literal keywords) {id=LiteralKeywords}

1. **[null](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/null)** — указывает отсутствие значения у ссылочных типов и значимых типов с поддержкой `null`. Используется, чтобы задать переменную как неинициализированную.

2. **[true](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/bool)** и **false** — логические литералы, обозначающие истину и ложь. Используются в логических выражениях и условиях для управления выполнением кода и связаны с типом `bool`.

3. **[default](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/default)** — возвращает значение по умолчанию для указанного типа и также применяется как "запасной" вариант в `switch`, чтобы обрабатывать все необъявленные варианты.

### Контекстные ключевые слова (Contextual Keywords) {id=ContextualKeywords}

Контекстные ключевые слова в C# - это слова, имеющие особое значение в определенных контекстах, но не являющиеся зарезервированными. 
Они могут использоваться как идентификаторы в других случаях.

1. **[add](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/add) / [remove](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/remove)**  
   Используются для определения методов добавления (`add`) и удаления (`remove`) обработчиков событий в пользовательских реализациях событий.

2. **get / set / init**  
   Эти ключевые слова определяют аксессоры свойств:
   - [get](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/get) — возвращает значение свойства.
   - [set](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/get) — устанавливает значение свойства.
   - [init](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/init) — устанавливает значение только при инициализации объекта, что добавлено в C# 9.0.

3. **partial ([type](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/partial-type) / [member](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/partial-member))**  
   Позволяет разделять определение типа (класса, структуры, интерфейса) или метода на несколько файлов, что полезно для крупных классов или генерируемого кода.

4. **[when](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/when)**  
   Используется в выражениях фильтрации в `catch` и в паттерн-матчинге (`switch`), для указания условий выполнения.

5. **[value](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/value)**  
   Используется в сеттерах свойств или индексаторов для обозначения присваиваемого значения.

6. **[required](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/value)**  
   Введено в C# 11. Этот модификатор указывает, что свойство обязательно должно быть инициализировано при создании объекта.  
   Например:

   ```c#
   public class Product
   {
       public required string Name { get; set; }
       public decimal Price { get; set; }
   }

   var product = new Product { Price = 100m }; // Ошибка: Name не инициализировано
   ```

   - **Особенности**:
      - Применяется только к свойствам и полям, объявленным как `public`.
      - Требует наличия конструктора, обеспечивающего инициализацию.
      - Улучшает безопасность кода, заставляя инициализировать все обязательные поля.

Контекстные ключевые слова предоставляют дополнительные возможности в языке C#, делая код более читаемым и удобным для поддержки.

### Ключевые слова запроса (Query keywords) {id=QueryKeywords}

Ключевые слова запросов (Query Keywords) в C# предназначены для выполнения операций с данными с использованием LINQ (Language Integrated Query). Они позволяют писать запросы, похожие на SQL, для работы с коллекциями, массивами и другими источниками данных. Рассмотрим их все:

1. **[from](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/from-clause)**
- **Описание**: Указывает источник данных и объявляет переменную для итерации.
- **Пример**:
  ```c#
  var result = from num in numbers select num;
  ```
  Здесь `num` — это текущий элемент коллекции `numbers`.

2. **[where](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/where-clause)**
- **Описание**: Фильтрует элементы на основе условия.
- **Пример**:
  ```c#
  var result = from num in numbers where num > 10 select num;
  ```
  Возвращает элементы больше 10.

3. **[select](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/select-clause)**
- **Описание**: Указывает, какие элементы будут выбраны в результате запроса.
- **Пример**:
  ```c#
  var result = from num in numbers select num * 2;
  ```
  Возвращает каждый элемент, умноженный на 2.

4. **[group by](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/group-clause)**
- **Описание**: Группирует элементы по указанному критерию.
- **Пример**:
  ```c#
  var result = from p in products group p by p.CategoryId;
  ```
  Группирует товары по идентификатору категории.

5. **[into](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/into)**
- **Описание**: Используется для создания промежуточного результата, часто после группировки.
- **Пример**:
  ```c#
  var result = from p in products
               group p by p.CategoryId into g
               select new { Category = g.Key, Count = g.Count() };
  ```
  Создает промежуточную коллекцию с количеством товаров в каждой категории.

6. **[orderby](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/orderby-clause)**
- **Описание**: Сортирует результаты запроса.
- **Пример**:
  ```c#
  var result = from num in numbers orderby num ascending select num;
  ```
  Сортирует по возрастанию.

7. **[join](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/join-clause)** и **[on equals](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/on)**
- **Описание**: Выполняют внутреннее соединение двух коллекций.
- **Пример**:
  ```c#
  var result = from p in products
               join c in categories on p.CategoryId equals c.Id
               select new { p.Name, c.CategoryName };
  ```
  Объединяет коллекции `products` и `categories` по `CategoryId`.

8. **[let](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/let-clause)**
- **Описание**: Вводит переменную для хранения промежуточного значения.
- **Пример**:
  ```c#
  var result = from num in numbers
               let square = num * num
               where square > 100
               select square;
  ```
  Вычисляет квадрат числа и фильтрует значения больше 100.

9. **[in](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/in)**
- **Описание**: Используется в начале запроса для определения источника данных.
- **Пример**:
  ```c#
  var result = from number in numbers select number;
  ```

10. **[on](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/on)** и **[equals](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/equals)**
- **Описание**: Используются вместе в выражении `join` для указания условий соединения двух коллекций.
- **Пример**:
  ```c#
  var result = from p in products
               join c in categories on p.CategoryId equals c.Id
               select new { p.Name, c.CategoryName };
  ```

11. **[ascending](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/ascending)** и **[descending](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/descending)**
- **Описание**: Указывают направление сортировки. По умолчанию используется **ascending**.  Сортирует по убыванию.
- **Пример**:
  ```c#
  var result = from num in numbers orderby num descending select num;
  ```

12. **[by](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/by)**
- **Описание**: Используется в выражении `group by` для указания критерия группировки.
- **Пример**:
  ```c#
  var result = from p in products group p by p.CategoryId;
  ```
## Литералы
Литералы в C# — это значения, которые непосредственно указаны в коде. В C# есть несколько типов литералов:

1. **Целочисленные литералы** — представляют целые числа (`10`, `0b1010` — бинарный, `0x1A` — шестнадцатеричный).
2. **Вещественные литералы** — числа с плавающей точкой (`3.14`, `2.71F`). Также доступны бинарные вещественные литералы (например, `0b1.1p1`).
3. **Символьные литералы** — один символ в одинарных кавычках (`'A'`).
4. **Строковые литералы** — строки в двойных кавычках (`"Hello"`).
5. **Логические литералы** — значения `true` и `false`.
6. **Null-литерал** — значение `null`, обозначающее отсутствие объекта.

Для примера создадим простой консольный проект ex0011_literals в папке episode02. В Program.cs введите следующий код:

```c#
using System;

class Program
{
    static void Main()
    {
        // Целочисленные литералы
        int decimalLiteral = 10;           // Десятичный литерал
        int hexLiteral = 0x1A;             // Шестнадцатеричный литерал
        int binaryLiteral = 0b1010;        // Бинарный литерал

        // Вещественные литералы
        double doubleLiteral = 3.14;       // Десятичное значение
        float floatLiteral = 2.71F;        // С суффиксом 'F' для типа float

        // Символьные литералы
        char charLiteral = 'A';            // Символ в одинарных кавычках

        // Строковые литералы
        string stringLiteral = "Hello, C#!"; // Строка в двойных кавычках

        // Логические литералы
        bool trueLiteral = true;           // Логическое значение true
        bool falseLiteral = false;         // Логическое значение false

        // Null-литерал
        object nullLiteral = null;         // Значение null

        // Вывод всех литералов
        Console.WriteLine($"Целочисленные литералы: {decimalLiteral}, {hexLiteral}, {binaryLiteral}");
        Console.WriteLine($"Вещественные литералы: {doubleLiteral}, {floatLiteral}");
        Console.WriteLine($"Символьный литерал: {charLiteral}");
        Console.WriteLine($"Строковый литерал: {stringLiteral}");
        Console.WriteLine($"Логические литералы: {trueLiteral}, {falseLiteral}");
        Console.WriteLine($"Null-литерал: {nullLiteral}");
    }
}
```
Запустив программу на выполнение вы увидите примерно следующее:

![literals](Literals.png){ border-effect="line" }

Выполнение последне инструкций выдаст предупреждение, поскольку код вообще не любит налетать на null, но об этом вы 
узнаете чуть позже. И не раз столкнетесь в своей практике программирования.

Так же стоит заметить что сами строки в инструкциях вывода в консоль это тоже строковые литералы.

## Специальные символы

В C# существует [несколько специальных символов](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/tokens/), 
которые помогают управлять текстовыми данными, обозначать ключевые элементы и расширять возможности языка.

1. [Интерполированные строки](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/tokens/interpolated) (**$**)

Интерполированные строки, обозначаемые символом `$`, позволяют включать выражения внутри строки, которые будут вычислены при выполнении кода. Пример:

```c#
int age = 30;
string message = $"Age is {age}";  // Вывод: Age is 30
```
Такая конструкция упрощает работу с текстом и переменными в строках. Подробнее можно узнать из [документации](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated).

2. [Буквальные строки](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/tokens/verbatim) (**@**)

Символ `@` используется для создания вербатим строк, в которых игнорируются стандартные управляющие символы (например, `\n` или `\\`). Это удобно при работе с путями файлов или текстом, требующим точного отображения:

```c#
string path = @"C:\Users\Name\Documents";
```
Кроме того, символ `@` позволяет использовать ключевые слова как идентификаторы:

```c#
int @class = 5;  // Использование ключевого слова class как имени переменной
```
Подробнее об этом можно узнать [здесь](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/verbatim).

3. [Сырые строки](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/tokens/raw-string) (**""" """**)

Сырые строковые литералы позволяют создавать текстовые блоки без необходимости экранирования символов или использования 
символов новой строки. Они обозначаются тройными кавычками (`"""`) и появились в C#11. Пример:

```c#
string rawText = """
    This is a raw
    multiline string
    """;
```
Такие строки удобны при работе с JSON, XML или HTML, где много кавычек и специальных символов. Подробнее можно прочитать в [документации](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/raw-string).

4. Экранированные символы

C# поддерживает различные управляющие последовательности (экранированные символы), такие как:
- `\n` — новая строка
- `\t` — табуляция
- `\\` — обратная косая черта
- `\"` — двойная кавычка

Эти символы используются для форматирования строк и включения специальных символов без их прямого отображения в тексте. 
Полный список можно найти в [официальной документации](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens).

## Операторы и выражения

В C# **операторы** и **выражения** являются основными элементами языка программирования, которые используются для выполнения 
различных операций и вычислений.

Определения
- **Оператор** (operator) — это символ или ключевое слово, которое указывает на выполнение определенной операции над одним или несколькими операндами. Например, арифметические операторы (`+`, `-`), операторы сравнения (`==`, `!=`) и логические операторы (`&&`, `||`).
- **Операнд** (operand) — это элемент выражения, над которым выполняется операция. В программировании операнды могут быть значениями (например, числа или переменные), к которым применяются операторы (арифметические, логические и т.д.).
- **Выражение** (expression) — это комбинация операторов и операндов, которая вычисляется и возвращает значение. Пример выражения: `a + b`, где `a` и `b` — операнды, а `+` — оператор.

Например, в выражении:

```c#
int result = a + b;
```
- `a` и `b` — **операнды**;
- `+` — **оператор**.

В общем случае операнды и операторы совместно составляют выражение, результатом которого является новое значение или действие.

### 1. **Арифметические операторы (Arithmetic Operators)**
Используются для выполнения математических операций:
- `+` (сложение): `int result = 2 + 3; // 5`
- `-` (вычитание): `int result = 5 - 3; // 2`
- `*` (умножение): `int result = 2 * 3; // 6`
- `/` (деление): `int result = 6 / 3; // 2`
- `%` (остаток от деления): `int result = 5 % 2; // 1`
- `++` (инкремент): `int a = 1; a++; // a = 2`
- `--` (декремент): `int a = 2; a--; // a = 1`

### 2. **Операторы сравнения (Comparison Operators)**
Используются для сравнения значений:
- `==` (равно): `bool result = (5 == 5); // true`
- `!=` (не равно): `bool result = (5 != 3); // true`
- `>` (больше): `bool result = (5 > 3); // true`
- `<` (меньше): `bool result = (3 < 5); // true`
- `>=` (больше или равно): `bool result = (5 >= 5); // true`
- `<=` (меньше или равно): `bool result = (3 <= 5); // true`

### 3. **Логические операторы (Boolean Logical Operators)**
Работают с булевыми значениями:
- `&&` (логическое И): `bool result = true && false; // false`
- `||` (логическое ИЛИ): `bool result = true || false; // true`
- `!` (логическое НЕ): `bool result = !true; // false`

### 4. **Битовые операторы и операторы сдвига (Bitwise and Shift Operators)**
Работают на уровне битов:
- `&` (побитовое И): `int result = 5 & 3; // 1`
- `|` (побитовое ИЛИ): `int result = 5 | 3; // 7`
- `^` (побитовое XOR): `int result = 5 ^ 3; // 6`
- `~` (побитовое НЕ): `int result = ~5; // -6`
- `<<` (сдвиг влево): `int result = 1 << 2; // 4`
- `>>` (сдвиг вправо): `int result = 4 >> 1; // 2`

### 5. **Операторы равенства (Equality Operators)**
Проверяют равенство и неравенство:
- `==`: проверяет равенство значений.
- `!=`: проверяет неравенство значений.

### 6. **Оператор присваивания (Assignment Operator)**
- `=`: используется для присваивания значений переменным: `int a = 5;`.

### 7. **Оператор условного выражения (Conditional Operator)**
- `?:` (тернарный оператор): `string result = (a > b) ? "a больше" : "b больше";`.

### 8. **Оператор "nameof"**
- Возвращает имя переменной или свойства как строку: `string name = nameof(variable);`.

### 9. **Оператор "new"**
- Создает экземпляр объекта: `var obj = new MyClass();`.

### 10. **Оператор "is"**
- Проверяет совместимость типов: `if (obj is MyClass) { ... }`.

### 11. **Оператор "as"**
- Выполняет безопасное приведение типов: `MyClass obj = input as MyClass;`.

### 12. **Оператор "await"**
- Используется в асинхронных методах для ожидания завершения задачи: `await Task.Delay(1000);`.

### 13. **Оператор "??" (null-coalescing)**
- Возвращает значение левого операнда, если оно не `null`, иначе возвращает правый операнд: `var result = a ?? b;`.

### 14. **Оператор "??="**
- Присваивает значение, если оно `null`: `a ??= b;`.

### 15. **Оператор "!" (null-forgiving)**
- Используется для подавления предупреждений о возможном `null`: `string name = GetName()!;`.

### 16. **Операторы лямбда-выражений (Lambda Operators)**
- Используются для создания лямбда-выражений: `(x, y) => x + y`.

### 17. **Оператор "=>" (lambda operator)**
- Используется для создания лямбда-выражений: `Func<int, int> square = x => x * x;`.

### 18. **Оператор "with"**
- Используется для создания нового объекта на основе существующего: `var newObj = obj with { Property = newValue };`.

### 19. **Оператор "default"**
- Возвращает значение по умолчанию для типа: `int defaultInt = default;`.

### 20. **Оператор "sizeof"**
- Возвращает размер типа в байтах: `int size = sizeof(int);`.

### 21. **Оператор "stackalloc"**
- Используется для выделения памяти на стеке: `int* array = stackalloc int[10];`.

### 22. **Оператор "delegate"**
- Создает делегат: `Action action = delegate { Console.WriteLine("Hello"); };`.

### 23. **Оператор "switch"**
- Используется для выполнения различных действий в зависимости от значения выражения:
```c#
switch (value)
{
    case 1: Console.WriteLine("One"); break;
    case 2: Console.WriteLine("Two"); break;
    default: Console.WriteLine("Other"); break;
}
```

### 24. **Операторы "true" и "false"**
- Определяют логику явных преобразований к булевому значению в пользовательских типах.

### 25. **Оператор "in" и "out"**
- Используются для передачи аргументов по ссылке.

### 26. **Оператор "is" (Pattern Matching)**
- Проверяет соответствие шаблону: `if (obj is int i && i > 0) { ... }`.

### 27. **Операторы перегрузки (Operator Overloading)**
- Позволяют определять пользовательское поведение операторов для классов:
```c#
public static MyClass operator +(MyClass a, MyClass b) => new MyClass(a.Value + b.Value);
```

### 28. **Оператор "->" (указатели)**
- Используется для доступа к членам структуры через указатель:
```c#
MyStruct* ptr = &myStruct;
ptr->Field = 10;
```

### 29. **Оператор "namespace alias qualifier" (`::`)**
- Используется для доступа к членам пространства имен с использованием псевдонима:
```c#
global::System.Console.WriteLine("Hello");
```

### 30. **Оператор "typeof"**
- Возвращает `Type` объекта: `Type t = typeof(int);`.

### 31. **Оператор "checked" и "unchecked"**
- Используются для управления переполнением целых чисел:
```c#
int result = checked(a + b);
```

### 32. **Операторы коллекций (Collection Expressions)**
- Используются для создания коллекций:
```c#
var list = new List<int> { 1, 2, 3 };
```

### Приоритет и ассоциативность операторов
- **[Приоритет](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/operators/#operator-precedence)** операторов определяет порядок их выполнения в выражении. Например, умножение (`*`) и деление (`/`) имеют более высокий приоритет, чем сложение (`+`) и вычитание (`-`).
- **[Ассоциативность](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/operators/#operator-associativity)** определяет порядок выполнения операторов с одинаковым приоритетом. Например, для арифметических операторов ассоциативность — левая, т.е. выражение `a - b + c` интерпретируется как `(a - b) + c`.

Пример:
```c#
int result = 10 - 2 * 5; // Результат: 0, так как умножение выполняется раньше вычитания
```

### Вычисление операндов
В C# операнды вычисляются слева направо. Это важно учитывать при использовании функций или выражений с побочными эффектами.

Пример:
```c#
int a = 5;
int b = 10;
int result = a++ + b; // a увеличивается после вычисления, поэтому результат 15, а затем a становится 6
```

### Подробное описание операторов
Для полного описания всех операторов C#, включая примеры использования, вы можете ознакомиться в [документации Microsoft](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/).

## Типы

C# — это строго типизированный язык программирования, где каждая переменная и выражение должны иметь определённый тип 
данных во время компиляции. Это позволяет компилятору проверять совместимость типов и предотвращать ошибки, связанные 
с некорректными операциями над несовместимыми типами данных. **Строгое типизирование** (strong typing) подразумевает, 
что значения разных типов не могут быть использованы взаимозаменяемо без явного преобразования.
Например, сложение числа и строки без явного преобразования вызовет ошибку:

```c#
int number = 10;
string text = "Number: ";
string result = text + number.ToString(); // Требуется явное преобразование числа в строку

```

### Определение типов в C#

В C# **тип (Type)** — это описание структуры данных, а также операции, которые могут быть выполнены над этими данными. 
Типы данных в C# делятся на две большие категории: **типов значений** (Value types) и **ссылочных типов** (Reference types).

### Типы значений (Value types)
**Типы значений** хранят свои данные непосредственно в переменной. Они размещаются в стеке, что делает операции с ними
быстрыми и не требует сборки мусора. Примеры включают числовые типы, булев тип, символы, перечисления и структуры.

**[Типы значений](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-types) 
([Value types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-types))**
- Целочисленные типы (`int`, `byte`, `long` и т.д.)
- Типы с плавающей запятой (`float`, `double`, `decimal`)
- Булев тип (`bool`)
- Символьный тип (`char`)
- Структуры (`struct`)
- Перечисления (`enum`)

### Ссылочные типы (Reference types)
**Ссылочные типы** хранят ссылку на объект в памяти, а не само значение. Они размещаются в куче, что требует работы
сборщика мусора для управления памятью. Примеры включают классы, интерфейсы, делегаты, строки и массивы.

**[Ссылочные типы](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/reference-types) ([Reference types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/reference-types))**
- Классы (`class`)
- Интерфейсы (`interface`)
- Делегаты (`delegate`)
- Строки (`string`)
- Массивы (`array`)
- Записи (`record`)

### Разница между типами значений и ссылочными типами
| Характеристика             | Типы значений      | Ссылочные типы   |
|----------------------------|--------------------|------------------|
| Хранение данных            | В стеке            | В куче           |
| Копирование                | Полное копирование | Копируется ссылка|
| Поддержка null             | Только Nullable    | Допускается      |
| Управление памятью         | Не требует GC      | Требует GC       |

_GC - Garbage Collector (Сборщик мусора)_

### Стек и куча: что это такое?

**Стек (stack)** — это область памяти, которая используется для хранения временных данных, таких как локальные переменные 
и параметры функции. Данные в стеке хранятся по принципу LIFO (Last In, First Out — последним пришёл, первым вышел). 
Стек обеспечивает быструю аллокацию и деаллокацию памяти, но его размер ограничен.

**Куча (heap)** — это область памяти, используемая для хранения объектов, создаваемых в процессе выполнения программы. 
В отличие от стека, куча не имеет ограниченного размера, но работа с ней происходит медленнее из-за необходимости управления 
памятью (сборка мусора). В C# выделение памяти в куче управляется сборщиком мусора (Garbage Collector), 
который автоматически освобождает память, занятую ненужными объектами.

### Описание типов значений (Valute types)

1. **[Целочисленные типы](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/integral-numeric-types) ([Integral numeric types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types))**:
    - Используются для представления целых чисел различных диапазонов.
    - Таблица типов:

   | Тип      | Диапазон                          | Размер (бит) | Тип .NET       |
      |----------|----------------------------------|--------------|----------------|
   | `sbyte`  | -128 до 127                      | 8            | `System.SByte` |
   | `byte`   | 0 до 255                         | 8            | `System.Byte`  |
   | `short`  | -32,768 до 32,767                | 16           | `System.Int16` |
   | `ushort` | 0 до 65,535                      | 16           | `System.UInt16`|
   | `int`    | -2,147,483,648 до 2,147,483,647  | 32           | `System.Int32` |
   | `uint`   | 0 до 4,294,967,295               | 32           | `System.UInt32`|
   | `long`   | -9,223,372,036,854,775,808 до 9,223,372,036,854,775,807 | 64 | `System.Int64` |
   | `ulong`  | 0 до 18,446,744,073,709,551,615  | 64           | `System.UInt64`|

2. **[Числовые типы с плавающей запятой](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types) ([Floating-point numeric types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types))**:
    - Используются для представления чисел с дробной частью.
    - Таблица типов:

   | Тип       | Диапазон                                   | Размер (бит) | Тип .NET        |
      |-----------|--------------------------------------------|--------------|-----------------|
   | `float`   | ±1.5 x 10^-45 до ±3.4 x 10^38              | 32           | `System.Single` |
   | `double`  | ±5.0 x 10^-324 до ±1.7 x 10^308            | 64           | `System.Double` |
   | `decimal` | ±1.0 x 10^-28 до ±7.9 x 10^28 (высокая точность) | 128       | `System.Decimal`|

3. **[Встроенные числовые преобразования](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/numeric-conversions) ([Built-in numeric conversions](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/numeric-conversions))**:
    - C# поддерживает явные и неявные преобразования числовых типов. Например, преобразование `int` в `float` происходит автоматически, а вот преобразование `double` в `int` требует явного указания.

4. **[Булев тип](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/bool) ([bool](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/bool))**:
    - Используется для представления логических значений: `true` или `false`.
    - Размер: 1 байт.
    - Тип .NET: `System.Boolean`.

5. **[Символьный тип](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/char) ([char](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/char))**:
    - Представляет отдельный символ Unicode UTF-16
    - Размер: 2 байта.
    - Тип .NET: `System.Char`.

6. **[Перечисления](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/enum) ([enum](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/enum))**:
    - Используются для создания набора именованных констант, связанных с целочисленными значениями.
    - Тип .NET: `System.Enum`.

7. **[Структуры](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/struct) ([struct](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct))** и **[ref структуры](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/ref-struct) ([ref struct](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/ref-struct))**:
    - Структуры — это пользовательские типы значений, которые можно использовать для объединения нескольких полей данных.
    - `ref struct` — это структура, которая ограничена для использования в стеке, избегая выделения в куче.
    - Тип .NET: `System.ValueType`.

8. **[Кортежи](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples) ([tuples](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-tuples))**:
    - Позволяют объединить несколько значений разных типов в одну структуру, например `(int, string)`.
    - Тип .NET: `System.ValueTuple`.

9. **[Типы значений, допускающие значение NULL](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/nullable-value-types) ([Nullable value types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/nullable-value-types))**:
    - Позволяют значимым типам принимать значение `null`.
    - Обозначаются знаком `?`, например `int?`.

### Описание ссылочных типов:

1. **[class](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/class)** — основа объектно-ориентированного программирования, содержит поля, методы, свойства и события.
2. **[interface](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface)** — описывает контракт, который должен реализовать класс.
3. **[delegate](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types#the-delegate-type)** — тип, представляющий ссылку на метод.
4. **[record](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/record)** — новый тип в C#, предназначенный для создания неизменяемых объектов.
5. **[object](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types#the-object-type)** — базовый класс для всех типов в C#.
6. **[string](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types#the-string-type)** — специальный тип для работы со строками.
7. **[dynamic](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types#the-dynamic-type)** — позволяет изменять тип переменной во время выполнения.
8. **[Nullable reference types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/nullable-reference-types)** — ссылки, которые могут принимать значение `null`.
9. **[Collections](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/collections)** — структуры данных, такие как `List`, `Dictionary`.
10. **[Arrays](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/arrays)** — массивы, используемые для хранения фиксированного количества элементов одного типа.

### Тип void
- Тип [void](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/void) используется в сигнатурах методов, которые не возвращают значения.

### Неуправляемые типы (Unmanaged types)
- [Неуправляемые типы](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/unmanaged-types) 😊, которые не управляются сборщиком мусора C#. Включают в себя примитивные типы, указатели и типы структур, не содержащие ссылочных типов.

### Таблица значений по умолчанию
| Тип                             | Значение по умолчанию |
|---------------------------------|-----------------------|
| Ссылочные типы (`class`, `interface`) | `null`                |
| Целочисленные типы (`int`, `byte`)   | `0`                   |
| Типы с плавающей точкой (`float`)    | `0`                   |
| Логический тип (`bool`)              | `false`               |
| Символьный тип (`char`)              | `'\0'` (U+0000)       |
| Перечисления (`enum`)                | Значение `0`          |
| Структуры (`struct`)                 | Значения по умолчанию всех полей |
| Nullable типы (`int?`, `string?`)    | `null`                |

