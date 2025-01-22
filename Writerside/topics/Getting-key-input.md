# Получаем нажатую клавишу в C#

Иногда в приложении бывает нужно получить информацию о нажатых пользователем клавишах. Для этого используется метод [ReadKey()](https://learn.microsoft.com/ru-ru/dotnet/api/system.console.readkey).

## Что такое ReadKey() и зачем он нужен? {id="readkey_1"}

Метод `ReadKey()` в C# используется для считывания нажатой клавиши от пользователя в консольном приложении. Когда программа вызывает `ReadKey()`, она останавливается и ждёт, пока пользователь нажмёт любую клавишу. После этого метод возвращает информацию о нажатой клавише.

Представьте, что ваш компьютер спрашивает: *"Какая клавиша была нажата?"* – и ждёт ответа. Как только вы нажмёте, например, `A`, программа узнает об этом и может использовать эту информацию, например, для управления персонажем в игре или для выполнения команд.

## Как работает ReadKey()? {id="readkey_2"}

Вот простой пример кода:

```c#
using System;

class Program
{
    static void Main()
    {
        Console.Write("Нажмите любую клавишу: ");
        ConsoleKeyInfo key = Console.ReadKey(); // Ожидание ввода
        Console.WriteLine();
        Console.WriteLine("Вы нажали: {0}", key.Key);
    }
}
```

Когда программа доходит до `Console.ReadKey()`, она останавливается и ждёт ввода. Если вы нажмёте `B`, программа выведет:

```
Нажмите любую клавишу: B
Вы нажали: B
```

## Что ещё можно узнать о нажатой клавише?

Метод `ReadKey()` возвращает объект `ConsoleKeyInfo`, который содержит три важных свойства:
- `Key` – какая клавиша была нажата (например, `A`, `Enter`, `F1`).
- `KeyChar` – символ, который соответствует нажатой клавише (например, `a`, `b`, `1`).
- `Modifiers` – были ли нажаты дополнительные клавиши, такие как `Shift`, `Ctrl` или `Alt`.

Пример:
```c#
ConsoleKeyInfo key = Console.ReadKey();
Console.WriteLine("Key: {0}, Char: {1}, Modifiers: {2}", key.Key, key.KeyChar, key.Modifiers);
```

Если вы нажмёте `Shift + K`, программа выведет:
```
Key: K, Char: K, Modifiers: Shift
```

Если вы нажмёте `F12`, программа выведет:
```
Key: F12, Char: , Modifiers: 0
```
(символ отсутствует, потому что `F12` – функциональная клавиша, и у неё нет текстового представления).

## Где можно использовать ReadKey()?

Метод `ReadKey()` полезен в:
- В консольных играх (но совместно с медодом `Console.KeyAvailable()`), где игрок управляет персонажем, например, двигает космический корабль и стреляет в метеориты.
- В консольных программах с интерактивным меню, где пользователь выбирает опции с клавиатуры.
- Консольных утилитах, которые ожидают подтверждения перед продолжением.

Практика!

Создай консольное приложение `ex0077_readkey` при помощи шаблона `tinyconsole` в папке `episode02` и добавь его в
файл решения `episode02.sln`. Это можно сделать как в командной строке, так и в любой IDE.

Приведи Program.cs к следующему виду:

```c#
using System;

class Program
{
    static void Main()
    {
        WriteLine("Нажимайте клавиши. Для выхода нажмите Esc.");
        
        while (true)
        {
            ConsoleKeyInfo key = ReadKey(true); // true означает, что клавиша не будет отображаться в консоли
            WriteLine("Key: {0}, Char: {1}, Modifiers: {2}", key.Key, key.KeyChar, key.Modifiers);
            
            if (key.Key == ConsoleKey.Escape)
            {
                WriteLine("Вы нажали Esc. Завершаем программу...");
                break;
            }
        }
    }
}
```

Теперь программа будет постоянно выводить информацию о нажатых клавишах, пока вы не нажмёте `Esc`.

#### Пример вывода программы:

```
Нажимайте клавиши. Для выхода нажмите Esc.
Key: A, Char: A, Modifiers: Shift
Key: F, Char: f, Modifiers: Alt
Key: H, Char:, Modifiers: Shift, Control
Key: Z, Char: , Modifiers: Alt, Shift, Control
Key: D, Char: , Modifiers: Alt, Shift, Control
Key: Escape, Char: odifiers: None
Вы нажали Esc. Завершаем программу...
```

> Внимани! Если вы будете запускать программу из какой-либо IDE, в Windows Terminal или даже консоли cmd Windows, то эти программы могут 
> перехватывать нажатия некоторых комбинаций клавиш. Которые могут являться их горячими клавишами. Поэтому
> программа может их не отображать.
> {style="warning"}

## Как получать нажатия клавиш без остановки программы

Обычно, когда мы хотим считать нажатие клавиши в консоли, мы используем метод `Console.ReadKey()`. Но у него есть один большой недостаток — **он останавливает выполнение программы, пока пользователь не нажмёт клавишу**.

Представь, что ты пишешь игру, и твой герой должен двигаться, но программа зависает, пока ждёт нажатие кнопки. Это плохо! Чтобы этого избежать, есть два полезных метода:

✅ `Console.KeyAvailable` — проверяет, нажата ли клавиша, но **не останавливает программу**.  
✅ `Console.ReadKey(true)` — считывает клавишу, но **не показывает её в консоли**.

### Как это работает?

Когда программа выполняется, она продолжает работать в бесконечном цикле (например, в игровой логике). Но мы хотим, чтобы нажатие клавиши не тормозило весь процесс.

Давай попрактикуемся, падаван!

Создай консольное приложение `ex0078_readkey_available` при помощи шаблона `tinyconsole` в папке `episode02` и добавь его в
файл решения `episode02.sln`. Это можно сделать как в командной строке, так и в любой IDE.



```c#
using System;
using System.Threading;

class Program
{
    static void Main()
    {
        WriteLine("Нажимайте клавиши (Esc - выход).");

        while (true)
        {
            if (KeyAvailable) // Проверяем, есть ли нажатая клавиша
            {
                ConsoleKeyInfo key = ReadKey(true); // Читаем клавишу без вывода в консоль
                WriteLine($"Key: {key.Key}, Char: {key.KeyChar}, Modifiers: {key.Modifiers}");

                if (key.Key == ConsoleKey.Escape)
                {
                    WriteLine("Выход из программы...");
                    break;
                }
            }

            // Тут может выполняться другой код, например игровой цикл
            Thread.Sleep(100); // Задержка, чтобы процессор не перегружался
        }
    }
}
```
👉 Этот код не блокируется, если клавиша не нажата. Он просто выполняет основной цикл и проверяет, нажимает ли пользователь кнопку.

#### Возможный вывод программы:

```
Нажимайте клавиши (Esc - выход).
Key: S, Char: s, Modifiers: None
Key: F, Char: f, Modifiers: None
Key: S, Char: s, Modifiers: None
Key: D, Char: d, Modifiers: None
Key: F, Char: f, Modifiers: None
Key: H, Char: H, Modifiers: Alt, Shift
Key: J, Char: J, Modifiers: Alt, Shift
Key: K, Char: K, Modifiers: Alt, Shift
Key: L, Char: L, Modifiers: Alt, Shift
Key: Escape, Char: odifiers: None
Выход из программы...
```


### `Console.CancelKeyPress` — обработка Ctrl+C

Иногда пользователи могут случайно нажать **Ctrl + C**, и программа просто закроется. Но мы можем это предотвратить, добавив обработчик `Console.CancelKeyPress`.

**Как это работает?**  
Когда пользователь нажимает **Ctrl + C**, срабатывает событие `Console.CancelKeyPress`, и мы можем обработать его, например, показав сообщение перед выходом.

#### Пример:
```c#
using System;

class Program
{
    static void Main()
    {
        Console.CancelKeyPress += (sender, e) =>
        {
            Console.WriteLine("\nВы нажали Ctrl+C. Программа не будет закрыта!");
            e.Cancel = true; // Отменяем закрытие программы
        };

        Console.WriteLine("Нажмите Ctrl+C, чтобы протестировать обработку нажатия.");

        while (true)
        {
            // Бесконечный цикл, чтобы программа не завершалась сразу
        }
    }
}
```
👉 Теперь программа **не закроется при Ctrl+C**, а просто покажет сообщение.

### 🚀 Мини-игра: Космический корабль против метеоритов

Теперь давай создадим **простенькую консольную игру**, где ты управляешь **космическим кораблём (<=!=>)**, стреляешь снарядами `!` и сбиваешь падающие метеориты `*`. Ты же, падаван! Звёздный боец!

**📌 Как работает игра?**
- Корабль двигается **стрелками влево и вправо**.
- Выстрел — **пробел**.
- Метеориты падают сверху вниз.
- Если метеорит долетает до нижней линии `=`, он её разрушает (`=` → `+`).
- Если снаряд `!` попадает в метеорит `*`, метеорит исчезает, но сперва вызрывеется, на его месте последовательнро рисуются o затем O  и затем 0
- В самом нижу игрового поля должно отображаться количество сбитых метеоритов.
- Игра заканчивается когда все метеориты сбиты. Количество метеоритов должно быть 100.
- Если не все знаки = разрушены, то это победа.
- Если метеорит попадает в корабль, то корабль уничтожается и игра заканчивается. Это проажение.

Создай консольное приложение `ex0079_star_defender` при помощи шаблона `tinyconsole` в папке `episode02` и добавь его в
файл решения `episode02.sln`. Это можно сделать как в командной строке, так и в любой IDE.

Приведи Program.cs к следующему виду:

```c#
using System;
using System.Threading;
using System.Collections.Generic;

class SpaceGame
{
    static int width, height;
    static int shipX;
    static List<int[]> bullets = new List<int[]>();
    static List<int[]> meteors = new List<int[]>();
    static int meteorsDestroyed = 0;
    static int totalMeteors = 100;
    static char[,] field;
    static bool gameOver = false;
    static bool shipDestroyed = false;
    static List<int[]> explosions = new List<int[]>();
    static int shipExplosionStep = 0;
    static int meteorFallSpeed = 0;
    static HashSet<int> destroyedShieldPositions = new HashSet<int>();

    static void Main()
    {
        Clear();
        CursorVisible = false;

        width = WindowWidth;
        height = WindowHeight - 1;
        shipX = width / 2;

        field = new char[height, width];

        Thread inputThread = new Thread(ReadInput);
        inputThread.Start();

        while (!gameOver)
        {
            UpdateGame();
            DrawGame();
            Thread.Sleep(200);
        }

        SetCursorPosition(0, height / 2);
        WriteLine(shipDestroyed ? "Игра окончена!" : "Вы победили!");
    }

    static void ReadInput()
    {
        while (!gameOver && !shipDestroyed)
        {
            if (KeyAvailable)
            {
                ConsoleKeyInfo key = ReadKey(true);
                if (key.Key == ConsoleKey.LeftArrow && shipX > 1) shipX--;
                if (key.Key == ConsoleKey.RightArrow && shipX < width - 5) shipX++;
                if (key.Key == ConsoleKey.Spacebar) bullets.Add(new int[] { height - 3, shipX + 2 });
            }
        }
    }

    static void UpdateGame()
    {
        for (int y = 0; y < height; y++)
            for (int x = 0; x < width; x++)
                field[y, x] = ' ';

        if (!shipDestroyed && meteors.Count < totalMeteors && new Random().Next(0, 10) == 0)
        {
            int meteorX = new Random().Next(2, width - 2);
            meteors.Add(new int[] { 0, meteorX });
        }

        meteorFallSpeed++;
        if (meteorFallSpeed % 2 == 0)
        {
            for (int i = meteors.Count - 1; i >= 0; i--)
            {
                meteors[i][0]++;
                if (meteors[i][0] >= height - 2)
                {
                    destroyedShieldPositions.Add(meteors[i][1]);
                    meteors.RemoveAt(i);
                }
            }
        }

        for (int i = bullets.Count - 1; i >= 0; i--)
        {
            bullets[i][0]--;
            if (bullets[i][0] < 0) bullets.RemoveAt(i);
        }

        for (int i = meteors.Count - 1; i >= 0; i--)
        {
            for (int j = bullets.Count - 1; j >= 0; j--)
            {
                if (meteors[i][0] == bullets[j][0] && meteors[i][1] == bullets[j][1])
                {
                    explosions.Add(new int[] { meteors[i][0], meteors[i][1], 0 });
                    meteors.RemoveAt(i);
                    bullets.RemoveAt(j);
                    meteorsDestroyed++;
                    break;
                }
            }
        }

        for (int i = explosions.Count - 1; i >= 0; i--)
        {
            explosions[i][2]++;
            if (explosions[i][2] > 2) explosions.RemoveAt(i);
        }

        foreach (var meteor in meteors)
        {
            if (meteor[0] == height - 3 && (meteor[1] >= shipX && meteor[1] <= shipX + 4))
            {
                shipDestroyed = true;
                return;
            }
        }

        foreach (var meteor in meteors)
        {
            if (meteor[0] == height - 2)
                destroyedShieldPositions.Add(meteor[1]);
        }

        if (!shipDestroyed && meteorsDestroyed >= totalMeteors)
        {
            bool hasShieldLeft = false;
            for (int x = 0; x < width; x++)
            {
                if (!destroyedShieldPositions.Contains(x))
                {
                    hasShieldLeft = true;
                    break;
                }
            }

            if (hasShieldLeft)
            {
                gameOver = true;
                return;
            }
        }

        foreach (var meteor in meteors) field[meteor[0], meteor[1]] = '*';

        foreach (var bullet in bullets) field[bullet[0], bullet[1]] = '!';

        foreach (var explosion in explosions)
        {
            char explosionChar = explosion[2] switch
            {
                0 => 'o',
                1 => 'O',
                _ => '0',
            };
            field[explosion[0], explosion[1]] = explosionChar;
        }

        if (shipDestroyed)
        {
            if (shipExplosionStep < 4)
            {
                char[] explosionStages = { '_', '=', '+', '*' };
                for (int i = 0; i < 5; i++)
                    field[height - 3, shipX + i] = explosionStages[shipExplosionStep];
                shipExplosionStep++;
            }
            else
            {
                gameOver = true;
            }
        }
        else
        {
            int shipY = height - 3;
            field[shipY, shipX] = '<';
            field[shipY, shipX + 1] = '=';
            field[shipY, shipX + 2] = '!';
            field[shipY, shipX + 3] = '=';
            field[shipY, shipX + 4] = '>';
        }

        for (int x = 0; x < width; x++)
            field[height - 2, x] = destroyedShieldPositions.Contains(x) ? '+' : '=';

        string score = $"Сбитые метеориты: {meteorsDestroyed}/{totalMeteors}";
        for (int i = 0; i < score.Length && i < width; i++)
            field[height - 1, i] = score[i];
    }

    static void DrawGame()
    {
        SetCursorPosition(0, 0);
        for (int y = 0; y < height; y++)
        {
            for (int x = 0; x < width; x++)
                Write(field[y, x]);
            WriteLine();
        }
    }
}
```

✅ **В бой, падван!** 🚀💥

Запусти игру в консоли `dotnet run`.

Возможный вариант игры у тебя может выглядеть так на экране консоли.

![Космический корабль против метеорито](ex0079_starDefender.png){ border-effect="line"  thumbnail="true" width="700" }

Код игры пока может быть тебе не понятен. Просто наслаждайся игрой, падван! И да пребудет с тобой Сила!