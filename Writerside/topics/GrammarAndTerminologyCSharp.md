# Грамматика и терминология C# 

В обычном языке, основной единицей, несущей смысловую нагрузку, является предложение. Предложение может состоять из одного или более слов.

В большинстве языков конец повествовательного предложения, при написании, обозначается точкой.

## Инструкции
В C# аналогом предложения можно назвать инструкцию (statement), которая заканчивается точкой с запятой. Например:

```c#
Console.WriteLine("Hello, World.");
```
Инструкцию можно рассматривать как предписание компьютеру выполнить определенное действие. В примере выше это вывести в консоль фразу Hello World.

Следовательно, программа - это совокупность инструкций которые выполняют какую-либо задачу.

Давайте, например, рассмотрим простейшую задачу получения от пользователя двух чисел и затем вывода суммы этих двух чисел.

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

Создайте проект ex0010_sum_of_two в папке episode02. И введите приведенный выше код. Практика это всегда полезно.

![dotnet new console -h](SumOfTowNumbers01.png){ border-effect="line" }

И затем запустите программу. Пример запуска:

![dotnet new console -h](SumOfTowNumbers02.png){ border-effect="line" }

Возможно пока этот пример вам не покажется сильно простым, но сложность здесь может представлять блок преобразования строки в число. 

