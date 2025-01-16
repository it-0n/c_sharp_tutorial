# Класс StringBuilder

Работа со строками в программировании может быть увлекательной, но порой затратной для системы. Чтобы  работать с текстом, 
в .NET есть два два основных класса: **String** и **[StringBuilder](https://learn.microsoft.com/ru-ru/dotnet/fundamentals/runtime-libraries/system-text-stringbuilder)**. В этой статье мы подробно познакомимся с классом 
**StringBuilder** и научимся использовать его эффективно.

## Введение в StringBuilder {id="stringbuilder_1"}

**String** и **[StringBuilder](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.stringbuilder)** оба представляют последовательности символов, но работают по-разному.

### Основные различия:
1. **String неизменяемый.** Каждый раз, когда вы что-то меняете в строке, создаётся новая копия строки в памяти. Это медленно, особенно если у вас много изменений.
2. **[StringBuilder](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/stringbuilder) изменяемый.** Он позволяет изменять текст без создания новых объектов. Это экономит память и ускоряет работу, особенно при больших изменениях или циклах.

### Когда что использовать?
- **String** подойдёт, если:
    - Изменений текста немного.
    - Вы работаете с фиксированным количеством операций объединения (например, `str1 + str2`).
    - Вам нужно искать подстроки (`IndexOf`, `StartsWith`) — в StringBuilder таких методов нет.

- **StringBuilder** подойдёт, если:
    - Вы вносите много изменений в текст.
    - Количество изменений заранее неизвестно (например, текст растёт в цикле).

**Пример:**
```c#
// String: много изменений — плохо для производительности
string text = "";
for (int i = 0; i < 1000; i++)
{
    text += i.ToString() + ", ";
}

// StringBuilder: тот же код, но работает быстрее
var sb = new System.Text.StringBuilder();
for (int i = 0; i < 1000; i++)
{
    sb.Append(i).Append(", ");
}
string result = sb.ToString();
```

### Где найти StringBuilder? {id="stringbuilder_2"}
Он находится в пространстве имен **System.Text**. Чтобы не писать длинное имя типа, подключите это пространство:
```c#
using System.Text;
```

## Создание экземпляра объекта StringBuilder {id="stringbuilder_3"}

Для начала работы с **StringBuilder**, его нужно создать. Это можно сделать разными способами:

### Пример 1: пустой объект
```c#
var sb = new StringBuilder();
```

### Пример 2: с начальным текстом
```c#
var sb = new StringBuilder("Привет, мир!");
```

### Пример 3: с заданной ёмкостью
```c#
var sb = new StringBuilder(100); // Места для 100 символов
```

### Пример 4: с начальным текстом и ёмкостью
```c#
var sb = new StringBuilder("Начальный текст", 200);
```

## Работа с ёмкостью и длинной

Ёмкость (**Capacity**) — это количество символов, которые **StringBuilder** может вместить без перевыделения памяти. Длина (**Length**) — текущее количество символов в тексте.

### Пример: управление ёмкостью и длиной
```c#
var sb = new StringBuilder("Привет");
Console.WriteLine($"Длина: {sb.Length}, Ёмкость: {sb.Capacity}");

// Увеличим ёмкость
sb.Capacity = 50;
Console.WriteLine($"Новая ёмкость: {sb.Capacity}");

// Уменьшим длину
sb.Length = 3;
Console.WriteLine($"Новый текст: {sb}"); // Вывод: При
```

## Изменение строки StringBuilder {id="stringbuilder_4"}

**[Основные методы изменения строки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/stringbuilder#modifying-the-stringbuilder-string)**

| Метод                   | Описание                                | Пример                                   |  
|--------------------------|-----------------------------------------|------------------------------------------|  
| **Append**              | Добавляет текст в конец.               | `sb.Append("текст");`                   |  
| **AppendFormat**        | Добавляет текст с форматированием.     | `sb.AppendFormat("Число: {0}", 42);`    |  
| **Insert**              | Вставляет текст в указанное место.     | `sb.Insert(5, "вставка");`              |  
| **Remove**              | Удаляет часть текста.                  | `sb.Remove(3, 5);`                      |  
| **Replace**             | Заменяет подстроку на другую.          | `sb.Replace("мир", "вселенная");`       |  

У StringBuilder кроме этих основных методов, есть ещё [несколько других методов](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.stringbuilder?view=net-9.0#methods). Их мы рассмотрим чуть позже в этой статье.

### Пример: демонстрация основных методов
```c#
var sb = new StringBuilder("Привет, мир!");
sb.Append(" Как дела?");                         // Добавляем текст
sb.AppendFormat(" Сегодня {0:dd.MM.yyyy}.", DateTime.Now); // Форматируем
sb.Insert(7, "дорогой ");                        // Вставляем текст
sb.Remove(0, 7);                                 // Удаляем "Привет, "
sb.Replace("мир", "вселенная");                  // Заменяем "мир" на "вселенная"
Console.WriteLine(sb);                           // Вывод: дорогой вселенная! Как дела? Сегодня 12.01.2025.
```

## Преобразование объекта StringBuilder в строку {id="stringbuilder_5"}

Чтобы превратить **StringBuilder** в строку, используйте метод **ToString**:
```c#
var sb = new StringBuilder("Привет");
string text = sb.ToString();
Console.WriteLine(text); // Вывод: Привет
```

## Поиск текста в объекте StringBuilder

**StringBuilder** не поддерживает методы поиска вроде `IndexOf` или `Contains`. Однако есть обходные пути:

| Метод                                    | Описание                                     | Плюсы/Минусы                                               |  
|------------------------------------------|---------------------------------------------|------------------------------------------------------------|  
| Искать до добавления                     | Проверяем строку перед добавлением.         | Простая логика, но только до добавления.                   |  
| Преобразовать в строку и искать          | Применяем `ToString` и ищем в строке.       | Гибко, но затратно по памяти.                              |  
| Использовать `Chars[]` для последовательного поиска | Перебираем символы вручную.                  | Эффективно, но код сложнее.                                |  
| Преобразовать в строку, изменить и снова записать | Работает, но теряет преимущества StringBuilder.| Если количество изменений большое, то теряет эффективность |

### Примеры:

1. **Искать до добавления:**
```c#
if (!sb.ToString().Contains("Привет"))
    sb.Append("Привет");
```

2. **Преобразовать в строку:**
```c#
if (sb.ToString().IndexOf("мир") != -1)
    Console.WriteLine("Слово найдено!");
```

3. **Использовать Chars:**
```c#
bool found = false;
for (int i = 0; i < sb.Length; i++)
{
    if (sb[i] == 'м') found = true;
}
Console.WriteLine($"Символ 'м' найден: {found}");
```

4. **Преобразовать, изменить и вернуть:**
```c#
string temp = sb.ToString().Replace("мир", "вселенная");
sb.Clear().Append(temp);
```

Время практики, падаван!

Создай консольное приложение `ex0072_stringbuilder` при помощи шаблона `tinyconsole` в папке `episode02` и добавь его в
файл решения `episode02.sln`. Это можно сделать как в командной строке, так и в любой IDE.

Приведи Program.cs к следующему виду:

```c#
using System;
using System.Text;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        WriteLine("=== Демонстрация StringBuilder ===\n");

        // Создание StringBuilder
        StringBuilder sb = new StringBuilder("Привет, мир!");
        WriteLine($"Исходная строка: {sb}\n");

        // Настройка емкости и длины
        sb.Capacity = 50;  // Устанавливаем емкость
        WriteLine($"Емкость после установки: {sb.Capacity}");
        sb.Length = 6;  // Уменьшаем длину строки
        WriteLine($"После обрезки длины: {sb}\n");

        // Изменение строки (методы StringBuilder)
        sb.Append("! Как дела?");
        WriteLine($"Append: {sb}");

        sb.AppendFormat(" Сегодня {0}.", DateTime.Now.DayOfWeek);
        WriteLine($"AppendFormat: {sb}");

        sb.Insert(7, " Дорогой!");
        WriteLine($"Insert: {sb}");

        sb.Remove(6, 9);
        WriteLine($"Remove: {sb}");

        sb.Replace("!", "! Друзья!");
        WriteLine($"Replace: {sb}\n");

        // Преобразование StringBuilder в строку
        string result = sb.ToString();
        WriteLine($"Преобразованный в string: {result}\n");

        // Поиск текста в StringBuilder (четыре метода)

        // 1. Поиск перед добавлением
        string textToFind = "Привет";
        if (!sb.ToString().Contains(textToFind))
        {
            sb.Append(" Привет");
        }
        WriteLine($"Поиск перед добавлением: {sb}");

        // 2. Преобразование в строку и поиск IndexOf
        int index = sb.ToString().IndexOf("Сегодня");
        WriteLine($"IndexOf поиска 'Сегодня': {index}");

        // 3. Поиск через Chars[] (исправленный)
        bool found = false;
        string searchString = "Друзья";
        for (int i = 0; i <= sb.Length - searchString.Length; i++)
        {
            bool match = true;
            for (int j = 0; j < searchString.Length; j++)
            {
                if (sb[i + j] != searchString[j])
                {
                    match = false;
                    break;
                }
            }
            if (match)
            {
                found = true;
                break;
            }
        }
        WriteLine($"Поиск через Chars[]: {(found ? "Найдено" : "Не найдено")}");

        // 4. Преобразование StringBuilder в string, поиск и модификация
        string tempString = sb.ToString();
        if (tempString.Contains("Друзья"))
        {
            tempString = tempString.Replace("Друзья", "Товарищи");
            sb.Clear().Append(tempString);
        }
        WriteLine($"Изменение через строку: {sb}");

        // Дополнительно: Поиск через регулярные выражения (бонус)
        bool regexFound = Regex.IsMatch(sb.ToString(), @"\bТоварищи\b");
        WriteLine($"Поиск через RegEx: {(regexFound ? "Найдено" : "Не найдено")}");
    }
}
```

#### Вывод программы:
```
=== Демонстрация StringBuilder ===

Исходная строка: Привет, мир!

Емкость после установки: 50
После обрезки длины: Привет

Append: Привет! Как дела?
AppendFormat: Привет! Как дела? Сегодня Thursday.
Insert: Привет! Дорогой! Как дела? Сегодня Thursday.
Remove: Привет! Как дела? Сегодня Thursday.
Replace: Привет! Друзья! Как дела? Сегодня Thursday.

Преобразованный в string: Привет! Друзья! Как дела? Сегодня Thursday.

Поиск перед добавлением: Привет! Друзья! Как дела? Сегодня Thursday.
IndexOf поиска 'Сегодня': 26
Поиск через Chars[]: Найдено
Изменение через строку: Привет! Товарищи! Как дела? Сегодня Thursday.
Поиск через RegEx: Найдено
```

## Подробнее о методах StringBuilder {id="stringbuilder_6"}

Рассмотрим [StringBuilder](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.stringbuilder) поближе. Мое описание 
не заменит официальной документации. Но я надеюсь что оно поможет вам её лучше понять.

### Основные методы StringBuilder {id="stringbuilder_7"}

#### **Append – добавляет текст в конец** {id="append_1"}
Метод `Append` просто **доклеивает** данные в конец `StringBuilder`. Можно добавлять строки, символы, числа и даже объекты.

**Пример:**
```c#
StringBuilder sb = new StringBuilder("Привет");
sb.Append(", мир!");
Console.WriteLine(sb); // Привет, мир!
```

**Что можно добавить?**
- `string`
- `char`
- `int`, `double`, `bool` и другие числа
- `object` (автоматически вызывается `.ToString()`)

#### **AppendFormat – форматирует текст перед добавлением**
Этот метод похож на `string.Format()`, но сразу **вставляет форматированный текст в `StringBuilder`**.

**Пример:**
```c#
int age = 25;
StringBuilder sb = new StringBuilder();
sb.AppendFormat("Мне {0} лет", age);
Console.WriteLine(sb); // Мне 25 лет
```
Тут `{0}` – это **заполнитель**, который заменяется `age`. Можно вставлять несколько параметров:
```c#
sb.AppendFormat("Сегодня {0}, {1}", DateTime.Now.DayOfWeek, "отличная погода!");
```

#### **AppendJoin – объединяет элементы массива через разделитель**
Этот метод позволяет **склеивать массив строк (или других значений) через разделитель**.

**Пример:**
```c#
string[] words = { "яблоко", "банан", "вишня" };
StringBuilder sb = new StringBuilder();
sb.AppendJoin(", ", words);
Console.WriteLine(sb); // яблоко, банан, вишня
```
Можно использовать с числами:
```c#
sb.AppendJoin(" - ", new int[] { 1, 2, 3 }); // 1 - 2 - 3
```

#### **AppendLine – добавляет текст и перевод строки**
Отличается от `Append`, потому что **автоматически добавляет `\n`** (перенос строки).

**Пример:**
```c#
StringBuilder sb = new StringBuilder();
sb.AppendLine("Первая строка");
sb.AppendLine("Вторая строка");
Console.WriteLine(sb);
```
Вывод:
```
Первая строка
Вторая строка
```
Можно даже просто вызвать `sb.AppendLine();`, чтобы вставить пустую строку.

#### **CopyTo – копирует символы в массив**
Этот метод копирует кусок текста `StringBuilder` **в массив символов (`char[]`)**.

**Пример:**
```c#
StringBuilder sb = new StringBuilder("Hello, world!");
char[] buffer = new char[5];
sb.CopyTo(7, buffer, 0, 5);
Console.WriteLine(new string(buffer)); // world
```
**Как это работает?**
- `7` – с какой позиции копировать
- `buffer` – массив, куда копируем
- `0` – позиция в `buffer`, куда вставлять
- `5` – сколько символов взять

#### **Insert – вставляет текст в определённую позицию** {id="insert_1"}
Позволяет вставлять текст **не только в конец, но и в любое место строки**.

**Пример:**
```c#
StringBuilder sb = new StringBuilder("Привет мир!");
sb.Insert(7, "дорогой ");
Console.WriteLine(sb); // Привет дорогой мир!
```
- `7` – это позиция, **куда вставить** `"дорогой "`
- Всё, что **правее**, сдвигается

Можно вставлять **числа, символы, массивы символов и даже объекты**.

#### **Remove – удаляет часть текста** {id="remove_1"}
Этот метод позволяет **удалить кусок текста по позиции**.

**Пример:**
```c#
StringBuilder sb = new StringBuilder("Привет, дорогой друг!");
sb.Remove(7, 8);
Console.WriteLine(sb); // Привет, друг!
```
- `7` – позиция, **с которой начать удаление**
- `8` – **сколько символов удалить**

#### **Replace – заменяет один текст на другой** {id="replace_1"}
Этот метод **находит и заменяет все вхождения** определённой строки или символа.

**Пример:**
```c#
StringBuilder sb = new StringBuilder("Я люблю C#. C# – лучший язык!");
sb.Replace("C#", "Python");
Console.WriteLine(sb); // Я люблю Python. Python – лучший язык!
```
Можно менять **конкретные символы**:
```c#
sb.Replace('!', '?');
```

#### **Equals – сравнивает два StringBuilder**
Метод `Equals` сравнивает **два объекта `StringBuilder`**.

**Пример:**
```c#
StringBuilder sb1 = new StringBuilder("Привет");
StringBuilder sb2 = new StringBuilder("Привет");

Console.WriteLine(sb1.Equals(sb2)); // True
```
>**Важно:** `Equals` сравнивает **содержимое** `StringBuilder`, а не ссылки в памяти.
{style="warning"}


### **Перегрузки методов**

#### **`Append` – перегрузки**
| Перегрузка | Описание |
|------------|----------|
| `Append(string value)` | Добавляет строку |
| `Append(char value)` | Добавляет символ |
| `Append(int value)` | Добавляет число |
| `Append(object value)` | Добавляет объект (через `.ToString()`) |
| `Append(char[] value, int startIndex, int count)` | Добавляет часть массива символов |

#### **`Insert` – перегрузки**
| Перегрузка | Описание |
|------------|----------|
| `Insert(int index, string value)` | Вставляет строку |
| `Insert(int index, char value)` | Вставляет символ |
| `Insert(int index, int value)` | Вставляет число |
| `Insert(int index, object value)` | Вставляет объект |

#### **`Replace` – перегрузки**
| Перегрузка | Описание |
|------------|----------|
| `Replace(string oldValue, string newValue)` | Заменяет всю строку |
| `Replace(char oldChar, char newChar)` | Заменяет символы |
| `Replace(string oldValue, string newValue, int startIndex, int count)` | Заменяет в диапазоне |

#### **`Remove` – перегрузки**
| Перегрузка | Описание |
|------------|----------|
| `Remove(int startIndex, int length)` | Удаляет часть строки |

