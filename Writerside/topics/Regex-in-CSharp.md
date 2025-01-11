# Регулярные выражения в C#

В предыдущем разделе строк в C# мы уже коснулись темы регулярных выражений. На эту тему пишут целые книги. Понятное дело что в небольшой статье я не смогу раскрыть всю эту тему полностью. Здесь мы, чуть более подробно, узнаем и разберем как использовать регулярные выражения в C# на практике. После прочтения данной статьи вы получите более менее полное представление об этой теме и всегда сможете углубить свои знания, используя линки предоставленные в тексте статьи.

Рассматривайте эту статью, просто как более подробное раскрытие темы или даже начальные сведения по этой теме. По большому счету вы даже можете её сейчас пропустить и перейти к следующему разделу. А вернуться к ней можете когда у вас возникнет необходимость. Но всё рекомендую хотя бы просто ознакомиться с этим разделом.

[Регулярные выражения](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expressions) (или Regex) — это специальный синтаксис, который используется для поиска, проверки, извлечения или замены текста по шаблону. Они часто применяются, когда нужно найти текст, соответствующий определенным правилам, например, проверить email или извлечь номера телефонов из текста.

## Обзор регулярных выражений

Регулярные выражения — это язык, используемый для описания текстовых шаблонов. В C# их поддержка реализована в пространстве имен `System.Text.RegularExpressions`. Основные классы:
- `Regex` — основной класс для работы с регулярными выражениями.
- `Match` — результат выполнения регулярного выражения.
- `MatchCollection` — коллекция всех совпадений в тексте.

#### Пример: Найдем все числа в строке.

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string input = "У меня 2 яблока и 3 банана";
        string pattern = @"\d+";
        
        MatchCollection matches = Regex.Matches(input, pattern);
        
        foreach (Match match in matches)
        {
            Console.WriteLine(match.Value); // Выведет: 2 и 3
        }
    }
}
```

**Объяснение**:
- `@"\d+"` — строка содержащая регулярное выражение, где:
    - `@` перед строкой позволяет писать строку как есть, игнорируя экранирование символов.
    - `\d+` само регулярное выражение (шаблон), где:
        - `\d` означает "любая цифра".
        - `+` означает "один или несколько раз".
- `Regex.Matches` ищет все совпадения в тексте.


#### Пример: Найти все email-адреса в тексте.

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string text = "Контакты: user@example.com, admin@domain.org.";
        string pattern = @"[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}";

        MatchCollection matches = Regex.Matches(text, pattern);
        foreach (Match match in matches)
        {
            Console.WriteLine($"Найден email: {match.Value}");
        }
    }
}
```

**Объяснение**:
- `@"[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}"` — строка содержащая регулярное выражение описывающее структуру email, где:
    - `@` перед строкой позволяет писать строку как есть, игнорируя экранирование символов.
    - `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}` - само регулярное выражение (шаблон) с достаточно сложной структурой описывающе email.
- `Regex.Matches` — ищет все совпадения шаблона.

## Элементы языка регулярных выражений

[Элементы языка регулярных выражений](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-language-quick-reference) задают правила сопоставления текста с шаблоном. 

### 1. **Escape-последовательности символов** {id="1_1"}
[Escape-последовательности](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/character-escapes-in-regular-expressions) используются, чтобы найти специальные символы, такие как точка (.), звезда (*) или скобки, которые обычно означают что-то особенное в регулярных выражениях. Для этого перед символом ставится обратная косая черта (`\`).

**Пример**:
```c#
string pattern = @"\.";
string text = "Пример: 3.14";
Console.WriteLine(Regex.Match(text, pattern).Value); // Выведет "."
```

### 2. **Классы символов** {id="2_1"}
[Классы символов](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/character-classes-in-regular-expressions) позволяют указать набор символов, с которым можно провести совпадение. Например, `[a-z]` соответствует любой букве от "a" до "z".

**Пример**:
```c#
string pattern = @"[a-z]";
string text = "abc123";
Console.WriteLine(Regex.Match(text, pattern).Value); // Выведет "a"
```

### 3. **Привязки** {id="3_1"}
[Привязки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/anchors-in-regular-expressions) задают, где должно происходить совпадение в строке — в начале, в конце или в любом месте.

**Пример**:
```c#
string pattern = @"^abc";  // ^ — начало строки
string text = "abcdef";
Console.WriteLine(Regex.Match(text, pattern).Value); // Выведет "abc"
```

### 4. **Конструкции группировки** {id="4_1"}
[Группировка](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/grouping-constructs-in-regular-expressions) позволяет объединить несколько символов или частей выражения в одну единицу, которую можно использовать для более сложных операций.

**Пример**:
```c#
string pattern = @"(abc)\d";
string text = "abc3";
Console.WriteLine(Regex.Match(text, pattern).Groups[1].Value); // Выведет "abc"
```

### 5. **Квантификаторы** {id="5_1"}
[Квантификаторы](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/quantifiers-in-regular-expressions) определяют, сколько раз символ или группа символов могут повторяться.

**Пример**:
```c#
string pattern = @"a{2,3}";
string text = "aaab";
Console.WriteLine(Regex.Match(text, pattern).Value); // Выведет "aaa"
```

### 6. **Конструкции обратных ссылок** {id="6_1"}
[Обратные ссылки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/backreference-constructs-in-regular-expressions) позволяют ссылаться на ранее найденные группы в регулярном выражении.

**Пример**:
```c#
string pattern = @"(\d)\1";
string text = "22";
Console.WriteLine(Regex.Match(text, pattern).Value); // Выведет "22"
```

### 7. **Конструкции изменения** {id="7_1"}
[Конструкции изменения](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/alternation-constructs-in-regular-expressions) позволяют изменять поведение поиска, например, игнорировать регистр.

**Пример**:
```c#
string pattern = @"abc";
string text = "ABC";
Console.WriteLine(Regex.IsMatch(text, pattern, RegexOptions.IgnoreCase)); // Выведет "True"
```

### 8. **Подстановки** {id="8_1"}
[Подстановки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/substitutions-in-regular-expressions) позволяют заменять найденные части текста.

**Пример**:
```c#
string pattern = @"\d";
string text = "abc123";
string replaced = Regex.Replace(text, pattern, "#");
Console.WriteLine(replaced); // Выведет "abc###"
```

### 9. **Параметры регулярных выражений** {id="9_1"}
[Параметры регулярных выражений](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options) позволяют настраивать поведение поиска: игнорировать регистр, искать только по целым словам и т.д.

**Пример**:
```c#
string pattern = @"abc";
string text = "ABCabc";
Console.WriteLine(Regex.IsMatch(text, pattern, RegexOptions.IgnoreCase)); // Выведет "True"
```

### 10. **Другие конструкции** {id="10_1"}
Существуют [другие конструкции](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/miscellaneous-constructs-in-regular-expressions), такие как символы для работы с пробелами (`\s`), цифрами (`\d`) и другими специальными символами.

**Пример**:
```c#
string pattern = @"\d{3}";
string text = "123";
Console.WriteLine(Regex.Match(text, pattern).Value); // Выведет "123"
``` 

Каждая из этих конструкций помогает точнее и гибче искать и обрабатывать текст с помощью регулярных выражений. 
Далее мы их рассмотрим более подробно. Но, как я говорил в начале, эта статья не может претендовать на абсолютно полное
описание темы регулярных выражений. Однако я постараюсь лаконично описать основные [элементы регулярных выражений](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-language-quick-reference)
чтобы вы имели о них представление. 

## Escape-последовательности символов {id="escape_1"}

[Escape-последовательности](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/character-escapes-in-regular-expressions) позволяют ссылаться на специальные символы. Таблица ниже содержит практически полный список:

| Символ | Описание |
|--------|----------|
| `\a`   | Звонок (BEL), `\u0007`. |
| `\b`   | Возврат на одну позицию назад (BACKSPACE), `\u0008`, но вне классов символов — граница слова. |
| `\t`   | Табуляция (TAB), `\u0009`. |
| `\r`   | Возврат каретки (CR), `\u000D`. |
| `\v`   | Вертикальная табуляция (VT), `\u000B`. |
| `\f`   | Перевод страницы (FF), `\u000C`. |
| `\n`   | Новая строка (LF), `\u000A`. |
| `\e`   | Escape-символ (ESC), `\u001B`. |
| `\xNN` | Символ с шестнадцатеричным кодом ASCII. Например, `\x20` — пробел. |
| `\cX`  | Управляющий символ ASCII. Например, `\cC` — CTRL+C. |
| `\uNNNN` | Юникод-символ с шестнадцатеричным кодом. Например, `\u0041` — "A". |
| `\\`   | Экранирование символа `\`. |

Экранирование используется для специальных символов, например, `.` или `*`. Чтобы найти точку (`.`) в тексте, нужно записать её как `\.`.

#### Пример: Используем escape-последовательности для поиска точки в тексте. {id="escape_2"}
```c#
string pattern = @"\.";
string text = "Файл: report.docx";
Match match = Regex.Match(text, pattern);
Console.WriteLine(match.Value); // Выведет "."
```

#### Пример: Используем escape-последовательности для поиска символов перехода на новую строку.

```c#
string text = "Первая строка\nВторая строка";
string pattern = @"\n";

if (Regex.IsMatch(text, pattern))
{
    Console.WriteLine("Найдена новая строка!"); // Выведется сообщение
}
```

## Классы символов

[Классы символов](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/character-classes-in-regular-expressions) позволяют группировать символы, которые должны быть найдены.

### Таблица основных классов символов

| Символ    | Описание                                                                                             |
|-----------|------------------------------------------------------------------------------------------------------|
| `.`       | Любой символ, **кроме новой строки** (`\n`).                                                         |
| `[abc]`   | Любой символ из перечисленных: `a`, `b`, или `c`.                                                    |
| `[^abc]`  | Любой символ, **кроме** перечисленных: `a`, `b`, или `c`.                                            |
| `[a-z]`   | Любая строчная буква от `a` до `z`.                                                                  |
| `[A-Z]`   | Любая заглавная буква от `A` до `Z`.                                                                 |
| `[0-9]`   | Любая цифра от `0` до `9`.                                                                           |
| `[a-zA-Z]`| Любая буква: строчная или заглавная.                                                                 |
| `\d`      | Любая цифра от `0` до `9` (эквивалентно `[0-9]`).                                                    |
| `\D`      | Любой символ, **кроме цифры** (обратное `\d`).                                                       |
| `\w`      | Любая буква, цифра или символ подчеркивания `_` (эквивалентно `[a-zA-Z0-9_]`).                       |
| `\W`      | Любой символ, **кроме** букв, цифр или символа `_` (обратное `\w`).                                  |
| `\s`      | Любой пробельный символ: пробел, табуляция, новая строка (`\n`), возврат каретки (`\r`), и т. д.     |
| `\S`      | Любой символ, **кроме** пробельного (обратное `\s`).                                                 |
| `\b`      | **Граница слова**: позиция между символами, входящими и не входящими в слово.                        |
| `\B`      | **Не граница слова**: позиция, где нет границы слова.                                                |
| `\p{}`    | Символ, соответствующий указанной категории Unicode (например, `\p{L}` — любая буква).               |
| `\P{}`    | Символ, **не соответствующий** указанной категории Unicode (обратное `\p{}`).                        |

#### Пример: Найдем слова, которые начинаются с заглавной буквы.

```c#
string text = "Привет мир! Добро пожаловать.";
string pattern = @"\b[A-ZА-Я][a-zа-я]*\b";

MatchCollection matches = Regex.Matches(text, pattern);
foreach (Match match in matches)
{
    Console.WriteLine(match.Value); // Привет, Добро
}
```

#### Пример: Найдем все числа.
```c#
string pattern = @"[0-9]+"; // Найти все числа
string text = "Цена: 123 руб.";
Match match = Regex.Match(text, pattern);
Console.WriteLine(match.Value); // Выведет "123"
```

### Основные категории Unicode для `\p{}` и `\P{}`

В данной таблице указаны основные, но далеко не все категории Unicode.

| Категория  | Описание                                                                                             |
|------------|-----------------------------------------------------------------------------------------------------|
| `\p{L}`    | Любая буква.                                                                                        |
| `\p{Ll}`   | Строчная буква.                                                                                     |
| `\p{Lu}`   | Заглавная буква.                                                                                    |
| `\p{Nd}`   | Цифра.                                                                                              |
| `\p{P}`    | Знак препинания.                                                                                    |
| `\p{Z}`    | Пробельный символ.                                                                                  |
| `\p{C}`    | Другие символы (управляющие символы, незадействованные области и т. д.).                            |
| `\p{S}`    | Символы (математические, валютные и т. д.).                                                         |
| `\p{M}`    | Символы комбинирования (например, ударения или диакритические знаки).                               |

**Обратные версии**:
- `\P{L}`: Любой символ, **кроме** буквы.
- `\P{Nd}`: Любой символ, **кроме** цифры.

#### Примеры использования `\p{}` и `\P{}`

1. **Найти все буквы в тексте:**
   ```c#
   string pattern = @"\p{L}";
   ```

2. **Найти все нецифровые символы:**
   ```c#
   string pattern = @"\P{Nd}";
   ```

3. **Найти все пробельные символы Unicode:**
   ```c#
   string pattern = @"\p{Z}";
   ```

4. **Найти заглавные буквы:**
   ```c#
   string pattern = @"\p{Lu}";
   ```


## Привязки

[Привязки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/anchors-in-regular-expressions) (или атомарные утверждения нулевой ширины) определяют положение, где должно быть найдено соответствие. В отличие от символов или классов символов, привязки не потребляют символы в строке.

| **Привязка** | **Описание**                                                                                                                                                    |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `^`          | Соответствие должно находиться в начале строки. В многострочном режиме — в начале линии.                                                                        |
| `$`          | Соответствие должно находиться в конце строки или перед символом `\n`. В многострочном режиме — в конце линии.                                                 |
| `\A`         | Соответствие должно находиться только в начале строки (не зависит от многострочного режима).                                                                   |
| `\Z`         | Соответствие должно находиться в конце строки или перед символом `\n` в конце строки.                                                                          |
| `\z`         | Соответствие должно находиться исключительно в конце строки.                                                                                                  |
| `\G`         | Соответствие начинается с позиции, где закончилось предыдущее совпадение, или в начале строки, если совпадений не было.                                        |
| `\b`         | Соответствие должно находиться на границе слова.                                                                                                               |
| `\B`         | Соответствие **не** должно находиться на границе слова.                                                                                                        |


### 1. **Начало строки: `^`** {id="1_2"}
Указывает, что соответствие должно начаться с первого символа строки.

- **Пример**:
    ```c#
    string pattern = @"^Hello";
    string text = "Hello, World!";
    Console.WriteLine(Regex.IsMatch(text, pattern)); // True
    ```
- В многострочном режиме (`RegexOptions.Multiline`):
    ```c#
    string pattern = @"^World";
    string text = "Hello\nWorld";
    Console.WriteLine(Regex.IsMatch(text, pattern, RegexOptions.Multiline)); // True
    ```

### 2. **Конец строки: `$`** {id="2_2"}
Указывает, что соответствие должно находиться в конце строки.

- **Пример**:
    ```c#
    string pattern = @"World!$";
    string text = "Hello, World!";
    Console.WriteLine(Regex.IsMatch(text, pattern)); // True
    ```
- В многострочном режиме:
    ```c#
    string pattern = @"World$";
    string text = "Hello\nWorld";
    Console.WriteLine(Regex.IsMatch(text, pattern, RegexOptions.Multiline)); // True
    ```

### 3. **Только начало строки: `\A`**
Указывает, что соответствие возможно только в начале строки, независимо от многострочного режима.

- **Пример**:
    ```c#
    string pattern = @"\AHello";
    string text = "Hello, World!\nHello again";
    Console.WriteLine(Regex.IsMatch(text, pattern)); // True
    ```

### 4. **Конец строки или до конца символа новой строки: `\Z`**
Соответствие находится либо в конце строки, либо перед символом `\n`.

- **Пример**:
    ```c#
    string pattern = @"World\Z";
    string text = "Hello, World\n";
    Console.WriteLine(Regex.IsMatch(text, pattern)); // True
    ```

### 5. **Только конец строки: `\z`**
Соответствие возможно только в конце строки, без учета символов новой строки.

- **Пример**:
    ```c#
    string pattern = @"World!\z";
    string text = "Hello, World!";
    Console.WriteLine(Regex.IsMatch(text, pattern)); // True
    ```

### 6. **Непрерывные совпадения: `\G`**
Соответствие начинается с позиции, где закончилось предыдущее совпадение.

- **Пример**:
    ```c#
    string pattern = @"\G\d";
    string text = "123abc456";
    MatchCollection matches = Regex.Matches(text, pattern);
    foreach (Match match in matches)
        Console.WriteLine(match.Value); // 1, 2, 3
    ```

### 7. **Граница слова: `\b`**
Указывает границу слова (где слово начинается или заканчивается).

- **Пример**:
    ```c#
    string pattern = @"\bword\b";
    string text = "word boundaries in a sentence";
    Console.WriteLine(Regex.IsMatch(text, pattern)); // True
    ```

### 8. **Не на границе слова: `\B`**
Указывает, что соответствие не должно быть на границе слова.

- **Пример**:
    ```c#
    string pattern = @"\Bword";
    string text = "wordboundaries";
    Console.WriteLine(Regex.IsMatch(text, pattern)); // True
    ```

## Конструкции группировки

[Конструкции группировки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/grouping-constructs-in-regular-expressions) используются для выделения частей регулярного выражения и обработки их по отдельности. Они позволяют:
1. Сопоставлять подвыражения.
2. Применять квантификаторы к частям выражения.
3. Захватывать подстроки для последующего использования.
4. Извлекать части строки для обработки через свойства `Match.Groups`.

### Захватываемые и незахватываемые конструкции
- **Захватываемая конструкция** сохраняет сопоставленную подстроку, которая становится доступной через группы (`Groups`) в объекте `Match`.
- **Незахватываемая конструкция** выполняет сопоставление, но не сохраняет результат, что экономит память и время.

### Таблица конструкций группировки

| **Конструкция**                                              | **Захватываемая или незахватываемая** | **Описание**                                                                                   |
|--------------------------------------------------------------|---------------------------------------|-----------------------------------------------------------------------------------------------|
| `(подвыражение)`                                             | Захватываемая                        | Сопоставляет и захватывает часть строки.                                                      |
| `(?<имя>подвыражение)`                                       | Захватываемая                        | Сопоставляет и захватывает с использованием именованной группы.                               |
| `(?<имя1-имя2>подвыражение)`                                 | Захватываемая                        | Используется для сбалансированных групп.                                                      |
| `(?:подвыражение)`                                           | Незахватываемая                      | Сопоставляет, но не захватывает.                                                              |
| `(?имяПодвыражения-имяГруппы)`                              | Незахватываемая                      | Сбалансированное сопоставление групп.                                                         |
| `(?=подвыражение)`                                           | Незахватываемая                      | Утверждение положительного просмотра вперед нулевой ширины.                                   |
| `(?!подвыражение)`                                           | Незахватываемая                      | Утверждение отрицательного просмотра вперед нулевой ширины.                                   |
| `(?<=подвыражение)`                                          | Незахватываемая                      | Утверждение положительного просмотра назад нулевой ширины.                                    |
| `(?<!подвыражение)`                                          | Незахватываемая                      | Утверждение отрицательного просмотра назад нулевой ширины.                                    |
| `(?>подвыражение)`                                           | Незахватываемая                      | Атомарная группа.                                                                             |


### Подробное описание конструкций группировки

#### 1. **Сопоставляемые части выражения: `(подвыражение)`**
Захватывает указанное подвыражение и делает его доступным через индекс.

- **Пример**:
    ```c#
    string pattern = @"(\d{4})-(\d{2})-(\d{2})"; // Год-месяц-день
    string text = "2023-01-09";
    Match match = Regex.Match(text, pattern);
    Console.WriteLine(match.Groups[1].Value); // "2023"
    Console.WriteLine(match.Groups[2].Value); // "01"
    Console.WriteLine(match.Groups[3].Value); // "09"
    ```

#### 2. **Именованные сопоставленные части выражения: `(?<имя>подвыражение)`**
Захватывает указанное подвыражение с именем, чтобы обращаться к нему по имени.

- **Пример**:
    ```c#
    string pattern = @"(?<Year>\d{4})-(?<Month>\d{2})-(?<Day>\d{2})";
    string text = "2023-01-09";
    Match match = Regex.Match(text, pattern);
    Console.WriteLine(match.Groups["Year"].Value); // "2023"
    Console.WriteLine(match.Groups["Month"].Value); // "01"
    Console.WriteLine(match.Groups["Day"].Value); // "09"
    ```

#### 3. **Сбалансированные определения группы: `(?<имя1-имя2>подвыражение)`**
Используются для сложных сопоставлений, например, проверки балансировки скобок.

- **Пример**:
    ```c#
    string pattern = @"(?<Open>\()|(?<-Open>\))";
    string text = "(())";
    MatchCollection matches = Regex.Matches(text, pattern);
    int balance = 0;
    foreach (Match match in matches)
    {
        if (match.Groups["Open"].Success) balance++;
        if (match.Groups["Open"].Success) balance--;
    }
    Console.WriteLine(balance == 0); // True
    ```

#### 4. **Незахватываемые группы: `(?:подвыражение)`** {id="4_2"}
Сопоставляет, но не захватывает подвыражение.

- **Пример**:
    ```c#
    string pattern = @"(?:\d{3})-(\d{2})-(\d{2})";
    string text = "123-45-67";
    Match match = Regex.Match(text, pattern);
    Console.WriteLine(match.Groups[1].Value); // "45"
    Console.WriteLine(match.Groups[2].Value); // "67"
    ```

#### 5. **Параметры группы: `(?imnsx-imnsx:подвыражение)`**
Изменяет поведение сопоставления внутри группы.

- **Пример**:
    ```c#
    string pattern = @"(?i:abc)"; // Регистр игнорируется
    string text = "ABC";
    Console.WriteLine(Regex.IsMatch(text, pattern)); // True
    ```

#### 6. **Утверждения положительного просмотра вперед: `(?=подвыражение)`**
Соответствует, если за текущей позицией следует указанное подвыражение.

- **Пример**:
    ```c#
    string pattern = @"\d+(?= USD)";
    string text = "100 USD";
    Match match = Regex.Match(text, pattern);
    Console.WriteLine(match.Value); // "100"
    ```

#### 7. **Утверждения отрицательного просмотра вперед: `(?!подвыражение)`**
Соответствует, если за текущей позицией **не следует** указанное подвыражение.

- **Пример**:
    ```c#
    string pattern = @"\d+(?! USD)";
    string text = "100 EUR";
    Match match = Regex.Match(text, pattern);
    Console.WriteLine(match.Value); // "100"
    ```

#### 8. **Утверждения положительного просмотра назад: `(?<=подвыражение)`**
Соответствует, если перед текущей позицией есть указанное подвыражение.

- **Пример**:
    ```c#
    string pattern = @"(?<=USD )\d+";
    string text = "USD 100";
    Match match = Regex.Match(text, pattern);
    Console.WriteLine(match.Value); // "100"
    ```

#### 9. **Утверждения отрицательного просмотра назад: `(?<!подвыражение)`**
Соответствует, если перед текущей позицией **нет** указанного подвыражения.

- **Пример**:
    ```c#
    string pattern = @"(?<!USD )\d+";
    string text = "EUR 100";
    Match match = Regex.Match(text, pattern);
    Console.WriteLine(match.Value); // "100"
    ```

#### 10. **Атомарные группы: `(?>подвыражение)`**
Сопоставляет выражение без возвратов (backtracking).

- **Пример**:
    ```c#
    string pattern = @"(?>a|aa)a";
    string text = "aa";
    Console.WriteLine(Regex.IsMatch(text, pattern)); // False
    ```

## Квантификаторы

[Квантификаторы](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/quantifiers-in-regular-expressions) — это элементы синтаксиса регулярных выражений, которые определяют количество повторений символа, группы или класса символов, необходимое для сопоставления с входными данными. Они позволяют задавать диапазоны, ограничивать количество повторений и управлять поведением поиска.

Квантификаторы позволяют задавать гибкие правила для поиска совпадений в тексте. Понимание разницы между жадными и ленивыми квантификаторами помогает эффективно контролировать поведение регулярных выражений и предотвращать избыточное захватывание символов.

### Таблица квантификаторов в .NET

| Жадный квантификатор | Ленивый квантификатор | Описание                                   |
|-----------------------|-----------------------|-------------------------------------------|
| `*`                  | `*?`                 | Соответствует нулю или более раз.         |
| `+`                  | `+?`                 | Соответствует одному или более раз.       |
| `?`                  | `??`                 | Соответствует нулю или одному разу.       |
| `{n}`                | `{n}?`               | Соответствует ровно `n` раз.              |
| `{n,}`               | `{n,}?`             | Соответствует по крайней мере `n` раз.    |
| `{n,m}`              | `{n,m}?`            | Соответствует от `n` до `m` раз.          |

### Жадные и ленивые квантификаторы

- **Жадные квантификаторы** (по умолчанию): Стремятся захватить как можно больше символов, которые соответствуют шаблону.
- **Ленивые квантификаторы** (с `?`): Стремятся захватить минимально возможное количество символов.

**Пример:**
```c#
string text = "abc123xyz";
string patternGreedy = @"\w+";
string patternLazy = @"\w+?";

Console.WriteLine(Regex.Match(text, patternGreedy).Value); // Вывод: "abc123xyz" (жадный захват)
Console.WriteLine(Regex.Match(text, patternLazy).Value);  // Вывод: "a" (ленивый захват)
```

### Квантификаторы и пустые соответствия

Квантификаторы могут приводить к совпадениям с пустыми строками, особенно если используется `*`, `?` или `{n,}`. Чтобы избежать неожиданных совпадений, следует использовать более строгие шаблоны.

**Пример:**
```c#
string text = "abc";
string pattern = @"\w*";
MatchCollection matches = Regex.Matches(text, pattern);

foreach (Match match in matches)
{
    Console.WriteLine($"'{match.Value}'"); 
    // Вывод: 'abc', '', '', (пустые строки между символами)
}
```

#### Примеры использования квантификаторов

1. **`*` — Ноль или более раз**:
   ```c#
   string pattern = @"a*";
   string text = "aaaab";
   Match match = Regex.Match(text, pattern);
   Console.WriteLine(match.Value); // "aaaa"
   ```

2. **`+` — Один или более раз**:
   ```c#
   string pattern = @"a+";
   string text = "aaaab";
   Match match = Regex.Match(text, pattern);
   Console.WriteLine(match.Value); // "aaaa"
   ```

3. **`?` — Ноль или один раз**:
   ```c#
   string pattern = @"colou?r";
   string text = "color colour";
   MatchCollection matches = Regex.Matches(text, pattern);
   foreach (Match match in matches)
       Console.WriteLine(match.Value); // "color", "colour"
   ```

4. **`{n}` — Ровно `n` раз**:
   ```c#
   string pattern = @"\d{4}";
   string text = "Year: 2023";
   Match match = Regex.Match(text, pattern);
   Console.WriteLine(match.Value); // "2023"
   ```

5. **`{n,}` — По крайней мере `n` раз**:
   ```c#
   string pattern = @"\d{2,}";
   string text = "12345";
   Match match = Regex.Match(text, pattern);
   Console.WriteLine(match.Value); // "12345"
   ```

6. **`{n,m}` — От `n` до `m` раз**:
   ```c#
   string pattern = @"\d{2,4}";
   string text = "12345";
   Match match = Regex.Match(text, pattern);
   Console.WriteLine(match.Value); // "1234"
   ```

#### Пример разницы между жадными и ленивыми квантификаторами

**Жадный поиск:**
```c#
string pattern = @"<.*>";
string text = "<div>Hello</div>";
Console.WriteLine(Regex.Match(text, pattern).Value); // "<div>Hello</div>"
```

**Ленивый поиск:**
```c#
string pattern = @"<.*?>";
string text = "<div>Hello</div>";
Console.WriteLine(Regex.Match(text, pattern).Value); // "<div>"
```

## Конструкции обратных ссылок

[Конструкции обратных ссылок](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/backreference-constructs-in-regular-expressions) — это механизм регулярных выражений, который позволяет повторно использовать уже найденные части строки. Если в выражении используется группа (часть выражения, заключенная в круглые скобки), обратные ссылки могут ссылаться на совпадение этой группы и использовать его снова.

Обратные ссылки полезны, когда нужно найти повторяющиеся фрагменты текста, такие как одинаковые слова, повторяющиеся символы или структуры, например HTML-теги.

### Нумерованные обратные ссылки

[Нумерованные обратные ссылки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/backreference-constructs-in-regular-expressions#numbered-backreferences) позволяют ссылаться на группы по их порядковому номеру. Нумерация групп начинается с **1**, а группа с номером **0** соответствует всему выражению.

#### Синтаксис
- `\1`, `\2`, `\3` и т. д. — соответствуют первой, второй, третьей группе и так далее.

#### Таблица использования

| Конструкция | Описание                             |
|-------------|-------------------------------------|
| `\1`        | Ссылается на первую группу.         |
| `\2`        | Ссылается на вторую группу.         |
| `\3`        | Ссылается на третью группу.         |

#### Пример
```c#
using System;
using System.Text.RegularExpressions;

string pattern = @"(\w+)\s+\1";
string text = "hello hello world";
bool isMatch = Regex.IsMatch(text, pattern);
Console.WriteLine(isMatch); // True
```

**Объяснение**:
1. `(\w+)` — находит слово (состоит из букв, цифр или `_`).
2. `\s+` — один или несколько пробелов.
3. `\1` — совпадает с тем же словом, что было найдено первой группой.

### Именованные обратные ссылки

[Именованные обратные ссылки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/backreference-constructs-in-regular-expressions#named-backreferences) позволяют задавать имена для групп, а затем ссылаться на них по имени. Это упрощает чтение и понимание сложных выражений.

#### Синтаксис
- Назначение имени: `(?<имя>...)`
- Ссылка на группу: `\k<имя>` или `\k'имя'`

#### Таблица использования

| Конструкция       | Описание                             |
|-------------------|-------------------------------------|
| `(?<name>...)`    | Определяет группу с именем `name`.   |
| `\k<name>`        | Ссылается на группу с именем `name`. |

#### Пример
```c#
using System;
using System.Text.RegularExpressions;

string pattern = @"(?<word>\w+)\s+\k<word>";
string text = "repeat repeat";
bool isMatch = Regex.IsMatch(text, pattern);
Console.WriteLine(isMatch); // True
```

**Объяснение**:
1. `(?<word>\w+)` — группа с именем `word`, которая находит слово.
2. `\k<word>` — совпадает с тем же словом, что найдено группой `word`.

### Именованные числовые обратные ссылки

[.NET позволяет ссылаться на группы как по имени, так и по номеру](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/backreference-constructs-in-regular-expressions#named-numeric-backreferences), если группе задано имя.

#### Синтаксис
- Ссылка по номеру: `\1`, `\2`.
- Ссылка по имени: `\k<имя>`.

#### Пример
```c#
using System;
using System.Text.RegularExpressions;

string pattern = @"(?<digit>\d+)\s+\k<digit>";
string text = "123 123";
bool isMatch = Regex.IsMatch(text, pattern);
Console.WriteLine(isMatch); // True
```

**Объяснение**:
1. `(?<digit>\d+)` — группа с именем `digit`, которая находит числа.
2. `\k<digit>` — совпадает с тем же числом, что найдено группой `digit`.

### С чем сопоставляются обратные ссылки

[Обратные ссылки сопоставляются с содержимым группы, найденным ранее в тексте](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/backreference-constructs-in-regular-expressions#what-backreferences-match). Если группа не нашла совпадения, обратная ссылка также не найдет его.

#### Пример 1: Успешное сопоставление {id="1_3"}
```c#
string pattern = @"(\w+)\s+\1";
string text = "word word";
Console.WriteLine(Regex.IsMatch(text, pattern)); // True
```

#### Пример 2: Неуспешное сопоставление {id="2_3"}
```c#
string pattern = @"(\w+)\s+\1";
string text = "word another";
Console.WriteLine(Regex.IsMatch(text, pattern)); // False
```

**Объяснение**:
- В первом примере группа `(\w+)` нашла слово `word`, и обратная ссылка `\1` совпала с тем же словом.
- Во втором примере слова разные, поэтому совпадения нет.

## Конструкции изменения

[Конструкции изменения](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/alternation-constructs-in-regular-expressions) в регулярных выражениях используются для создания гибких шаблонов, позволяющих выбирать между несколькими альтернативами или проверять условные совпадения. Эти конструкции включают операторы "ИЛИ" (`|`) и условия, которые проверяют, выполнены ли определенные группы или выражения.

### Сопоставление шаблонов с `|`

[Конструкция сопоставления шаблонов с `|`](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/alternation-constructs-in-regular-expressions) обозначает логическое "ИЛИ", позволяя выбрать одно из нескольких подвыражений.

#### Синтаксис
- `A|B` — соответствует либо шаблону `A`, либо шаблону `B`.

#### Пример 1: Простое использование {id="1_4"}
```c#
using System;
using System.Text.RegularExpressions;

string pattern = @"cat|dog";
string text = "I have a dog";
bool isMatch = Regex.IsMatch(text, pattern);
Console.WriteLine(isMatch); // True
```

**Объяснение**:
- Шаблон `cat|dog` ищет либо слово "cat", либо слово "dog".
- В данном тексте найдено "dog".

#### Пример 2: Более сложное выражение {id="2_4"}
```c#
string pattern = @"(red|blue) car";
string text = "I saw a blue car";
bool isMatch = Regex.IsMatch(text, pattern);
Console.WriteLine(isMatch); // True
```

**Объяснение**:
- Шаблон `(red|blue) car` находит либо "red car", либо "blue car".
- В тексте найдено "blue car".

### Условное сопоставление с выражением

[Условные сопоставления с выражением](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/alternation-constructs-in-regular-expressions#conditional-matching-with-an-expression) проверяют, выполнено ли определенное условие, и выбирают подходящий шаблон для сопоставления.

#### Синтаксис
- `(?(условие)шаблон1|шаблон2)` — проверяет условие:
    - Если условие выполнено, используется `шаблон1`.
    - Если нет — `шаблон2`.

#### Таблица использования

| Конструкция                     | Описание                                             |
|---------------------------------|-----------------------------------------------------|
| `(?<name>...)`                  | Определяет именованную группу.                      |
| `(?(expression)pattern1|pattern2)` | Условное выражение для проверки логического выражения. |

#### Пример: Проверка логического условия
```c#
string pattern = @"(?(?=\d{4})\d{4}-\d{4}|\d{3}-\d{3})";
string text1 = "1234-5678";
string text2 = "123-456";

Console.WriteLine(Regex.IsMatch(text1, pattern)); // True
Console.WriteLine(Regex.IsMatch(text2, pattern)); // True
```

**Объяснение**:
- `(?=\d{4})` — проверяет, начинается ли строка с четырех цифр.
- Если условие выполнено, используется шаблон `\d{4}-\d{4}`.
- Иначе — шаблон `\d{3}-\d{3}`.

### Условное сопоставление на основе действительной захватываемой группы

[Этот тип конструкций](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/alternation-constructs-in-regular-expressions#conditional-matching-based-on-a-valid-captured-group) проверяет, была ли определенная группа успешно захвачена, и выбирает шаблон для сопоставления.

#### Синтаксис
- `(?(name)шаблон1|шаблон2)`:
    - Если группа `name` захватила значение, используется `шаблон1`.
    - Если нет — `шаблон2`.

#### Таблица использования

| Конструкция                     | Описание                                             |
|---------------------------------|-----------------------------------------------------|
| `(?<name>...)`                  | Определяет именованную группу.                      |
| `(?(name)pattern1|pattern2)`    | Проверяет, была ли группа `name` захвачена.         |

#### Пример: Проверка захваченной группы
```c#
string pattern = @"(?<word>\w+)?(?(word)\d{3}|\d{4})";
string text1 = "hello123";
string text2 = "4567";

Console.WriteLine(Regex.IsMatch(text1, pattern)); // True
Console.WriteLine(Regex.IsMatch(text2, pattern)); // True
```

**Объяснение**:
- `(?<word>\w+)?` — группа `word` захватывает слово (если оно есть).
- `(?(word)\d{3}|\d{4})`:
    - Если группа `word` найдена, ищет три цифры.
    - Если нет — четыре цифры.

## Подстановки

Когда вы используете метод **`Regex.Replace`**, вы можете указать шаблон для поиска (регулярное выражение) и строку для замены (подстановку).
[Подстановка](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/substitutions-in-regular-expressions) может быть простой (например, заменить пробелы на дефисы) или сложной, основанной на найденных частях текста.

### Пример:
```c#
using System.Text.RegularExpressions;

string pattern = @"\s+";  // Регулярное выражение для поиска пробелов
string replacement = "-"; // Замена на дефис
string text = "Много    пробелов";
string result = Regex.Replace(text, pattern, replacement);

Console.WriteLine(result); // Результат: "Много-пробелов"
```

### Элементы подстановки и шаблонов замены

| Элемент                  | Описание                                                                                      |
|--------------------------|-----------------------------------------------------------------------------------------------|
| `$number`                | [Нумерованная группа](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/substitutions-in-regular-expressions#substituting-a-numbered-group), соответствующая определённой части текста.                              |
| `${name}`                | [Именованная группа](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/substitutions-in-regular-expressions#substituting-a-named-group), соответствующая определённой части текста.                               |
| `$$`                     | [Символ `$`](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/substitutions-in-regular-expressions#substituting-a--character).                                                                                  |
| `$&`                     | [Весь текст](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/substitutions-in-regular-expressions#substituting-the-entire-match), который соответствует шаблону.                                                   |
| `$``                     | [Текст перед соответствием](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/substitutions-in-regular-expressions#substituting-the-text-before-the-match).                                                                   |
| `$'`                     | [Текст после соответствия](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/substitutions-in-regular-expressions#substituting-the-text-after-the-match).                                                                    |
| `$+`                     | [Последняя запомненная группа](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/substitutions-in-regular-expressions#substituting-the-last-captured-group).                                                                |
| `$_`                     | [Вся входная строка](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/substitutions-in-regular-expressions#substituting-the-entire-input-string).                                                                          |

### Подстановка нумерованной группы

Регулярные выражения позволяют выделять части текста в группы с помощью круглых скобок `()`. 
Эти группы можно использовать в подстановке с помощью `$1`, `$2` и так далее.

#### Пример:
```c#
string pattern = @"(\d{3})-(\d{2})-(\d{4})"; // Номер в формате XXX-XX-XXXX
string replacement = "($1) $2-$3";           // Переформатировать в (XXX) XX-XXXX
string text = "123-45-6789";
string result = Regex.Replace(text, pattern, replacement);

Console.WriteLine(result); // Результат: "(123) 45-6789"
```

### Подстановка именованной группы

Именованные группы определяются в регулярных выражениях с помощью `(?<name>...)`. 
Вы можете ссылаться на них в подстановке с помощью `${name}`.

#### Пример:
```c#
string pattern = @"(?<area>\d{3})-(?<prefix>\d{2})-(?<suffix>\d{4})";
string replacement = "(${area}) ${prefix}-${suffix}";
string text = "123-45-6789";
string result = Regex.Replace(text, pattern, replacement);

Console.WriteLine(result); // Результат: "(123) 45-6789"
```

### Подстановка знака `$`

Чтобы вставить символ `$` в строку замены, используйте `$$`.

#### Пример:
```c#
string pattern = @"\d+";
string replacement = "$$&"; // Добавляем символ $ перед числом
string text = "Цена 100 долларов";
string result = Regex.Replace(text, pattern, replacement);

Console.WriteLine(result); // Результат: "Цена $100 долларов"
```

### Подстановка всего соответствия

Используйте `$&`, чтобы вставить весь текст, который соответствует шаблону.

#### Пример:
```c#
string pattern = @"\b\w+\b"; // Найти каждое слово
string replacement = "<$&>"; // Обернуть слово в <>
string text = "Hello world";
string result = Regex.Replace(text, pattern, replacement);

Console.WriteLine(result); // Результат: "<Hello> <world>"
```

### Подстановка текста до соответствия

Используйте `$```, чтобы вставить текст, расположенный перед соответствием.

#### Пример:
```c#
string pattern = @"world";
string replacement = "[$`]";
string text = "Hello world";
string result = Regex.Replace(text, pattern, replacement);

Console.WriteLine(result); // Результат: "Hello [Hello ]"
```

### Подстановка текста после соответствия

Используйте `$'`, чтобы вставить текст, расположенный после соответствия.

#### Пример:
```c#
string pattern = @"Hello";
string replacement = "[$']";
string text = "Hello world";
string result = Regex.Replace(text, pattern, replacement);

Console.WriteLine(result); // Результат: "[ world] world"
```

### Подстановка последней записанной группы

Используйте `$+`, чтобы вставить последнюю записанную группу.

#### Пример:
```c#
string pattern = @"(cat)|(dog)";
string replacement = "[$+]";
string text = "I have a cat and a dog.";
string result = Regex.Replace(text, pattern, replacement);

Console.WriteLine(result); // Результат: "I have a [cat] and a [dog]."
```

### Замена всей входной строки

Используйте `$_`, чтобы вставить всю входную строку.

#### Пример:
```c#
string pattern = @"\b\w+\b";
string replacement = "[$_]";
string text = "Hello world";
string result = Regex.Replace(text, pattern, replacement);

Console.WriteLine(result); // Результат: "[Hello world] [Hello world]"
```

## Параметры регулярных выражений

**Что такое [параметры регулярных выражений](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options)?**

Параметры регулярных выражений позволяют настроить их работу под разные ситуации. Например, вы можете сделать так, 
чтобы поиск не учитывал регистр букв (а и А считались одинаковыми), или чтобы пробелы в шаблоне игнорировались. 
Эти параметры помогают гибко управлять поведением регулярного выражения, чтобы оно выполняло свои задачи максимально 
эффективно.

По умолчанию регулярные выражения различают заглавные и строчные буквы (например, "А" и "а" — это разные символы), 
а пробелы в шаблоне считаются важными. Также группы, создаваемые в выражении, можно использовать без явного указания. 
Но вы можете изменить это поведение с помощью параметров, чтобы, например, игнорировать регистр или пропускать пробелы.

**Параметры задаются либо прямо в шаблоне, либо в коде при создании регулярного выражения**.

### Виды параметров регулярных выражений

В зависимости от способа задания параметры делятся на две категории:

1. **Параметры, которые можно задать одновременно в строке и через код**:  
   Эти параметры можно включить как с помощью флагов в шаблоне (например, `(?i)`), так и через перечисление `RegexOptions` в коде.
    - **[RegexOptions.IgnoreCase](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regexoptions#system-text-regularexpressions-regexoptions-ignorecase)**: Игнорировать регистр.
    - **[RegexOptions.Multiline](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regexoptions#system-text-regularexpressions-regexoptions-multiline)**: Многострочный режим.
    - **[RegexOptions.Singleline](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regexoptions#system-text-regularexpressions-regexoptions-singleline)**: Однострочный режим.
    - **[RegexOptions.ExplicitCapture](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regexoptions#system-text-regularexpressions-regexoptions-explicitcapture)**: Только явные захваты.
    - **[RegexOptions.IgnorePatternWhitespace](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regexoptions#system-text-regularexpressions-regexoptions-ignorepatternwhitespace)**: Пропускать пробелы.

2. **Параметры, которые можно задать только через код**:  
   Эти параметры нельзя включить в строке. Они задаются через параметр `options` конструктора `Regex`.
    - **[RegexOptions.None](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regexoptions#system-text-regularexpressions-regexoptions-none)**: Использовать поведение по умолчанию.
    - **[RegexOptions.Compiled](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regexoptions#system-text-regularexpressions-regexoptions-compiled)**: Компилировать регулярное выражение.
    - **[RegexOptions.RightToLeft](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regexoptions#system-text-regularexpressions-regexoptions-righttoleft)**: Обратный поиск (справа налево).
    - **[RegexOptions.CultureInvariant](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regexoptions#system-text-regularexpressions-regexoptions-cultureinvariant)**: Игнорировать региональные различия.
    - **[RegexOptions.ECMAScript](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regexoptions#system-text-regularexpressions-regexoptions-ecmascript)**: Включить совместимость с ECMAScript.

### Таблица параметров регулярных выражений

| **Параметр**            | **Символ** | **Что делает**                                                                                                                                 |
|--------------------------|------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **`None`**              | —          | Использует стандартное поведение регулярных выражений.                                                                                        |
| **`IgnoreCase`**         | `i`        | Игнорирует регистр букв (например, "А" и "а" считаются одинаковыми).                                                                           |
| **`Multiline`**          | `m`        | Позволяет символам `^` и `$` обозначать начало и конец каждой строки, а не всей строки целиком.                                               |
| **`Singleline`**         | `s`        | Заставляет точку (`.`) соответствовать любому символу, включая символ новой строки (`\n`).                                                    |
| **`ExplicitCapture`**    | `n`        | Отключает неявное создание групп. Только именованные группы (`?<name>`) будут использоваться.                                                 |
| **`Compiled`**           | —          | Скомпилирует регулярное выражение для ускорения многократного использования.                                                                  |
| **`IgnorePatternWhitespace`** | `x`  | Игнорирует пробелы в шаблоне и позволяет добавлять комментарии.                                                                               |
| **`RightToLeft`**        | —          | Заставляет поиск выполняться справа налево.                                                                                                  |
| **`ECMAScript`**         | —          | Использует правила, совместимые с ECMAScript.                                                                                                |
| **`CultureInvariant`**   | —          | Игнорирует языковые и региональные особенности при сравнении.                                                                                 |
| **`NonBacktracking`**    | —          | Использует алгоритм без обратного отслеживания, чтобы обеспечить линейную сложность поиска. (Доступно с .NET 7 и выше.)                       |

### Указание параметров

[Параметры можно задать тремя способами](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#specify-options):
#### 1. **Через перечисление `RegexOptions`**

Параметры задаются при создании объекта `Regex` через аргумент `options`. Этот способ позволяет использовать перечисления, которые включают нужные параметры.

Пример:
```c#
Regex regex = new Regex("hello", RegexOptions.IgnoreCase | RegexOptions.Multiline);
Console.WriteLine(regex.IsMatch("HELLO")); // True
```

Здесь мы объединили несколько параметров, используя оператор `|` (побитовое OR).

#### 2. **Через комбинацию строкового шаблона и параметров `RegexOptions`**

Вы можете одновременно указать параметры в строке регулярного выражения и дополнить их параметрами через `RegexOptions`. В таком случае оба способа комбинируются и действуют вместе.

Пример:
```c#
string pattern = "(?m)hello"; // Включает многострочный режим.
Regex regex = new Regex(pattern, RegexOptions.IgnoreCase); // Дополнительно игнорирует регистр.
Console.WriteLine(regex.IsMatch("HELLO")); // True
```

Обратите внимание, что если параметры из строки и из `RegexOptions` противоречат друг другу, поведение может быть неопределенным.

#### 3. Задание параметров через строку-шаблон {id="3_3"}

##### Синтаксис:
В строке регулярного выражения параметры задаются с помощью конструкции:  
`(?imnsx-imnsx:часть выражения)`.

- **`i`** — Игнорирование регистра.
- **`m`** — Многострочный режим.
- **`n`** — Только явные захваты.
- **`s`** — Однострочный режим.
- **`x`** — Игнорирование пробелов в шаблоне и включение комментариев.

Можно как включать параметры, так и отключать их:
- Параметры включаются, если перед ними **нет знака минуса**.
- Параметры отключаются, если перед ними стоит **минус**.

Эта конструкция применяется только к определённой части выражения, заключённой в скобки.

##### Примеры:

##### Игнорирование регистра (`i`)
```c#
string pattern = "(?i)hello";
Regex regex = new Regex(pattern);
Console.WriteLine(regex.IsMatch("HELLO")); // True
```

##### Многострочный режим (`m`)
```c#
string pattern = "(?m)^hello$";
Regex regex = new Regex(pattern);
string input = "hello\nworld";
Console.WriteLine(regex.Matches(input).Count); // 1
```

##### Однострочный режим (`s`)
```c#
string pattern = "(?s).+";
Regex regex = new Regex(pattern);
string input = "hello\nworld";
Console.WriteLine(regex.IsMatch(input)); // True
```

##### Только явные захваты (`n`)
```c#
string pattern = "(?n)(?<name>hello)";
Regex regex = new Regex(pattern);
Console.WriteLine(regex.IsMatch("hello")); // True
```

##### Пропуск пробелов (`x`)
```c#
string pattern = @"(?x)
    h e l l o   # Комментарий: регулярка ищет 'hello'
";
Regex regex = new Regex(pattern);
Console.WriteLine(regex.IsMatch("hello")); // True
```

##### Комбинированный пример
Включение одних параметров и отключение других:
```c#
string pattern = @"(?im-s:hello)"; // Игнорируется регистр и включен многострочный режим, но отключен однострочный режим.
Regex regex = new Regex(pattern);
Console.WriteLine(regex.IsMatch("HELLO")); // True
```

#### Дополнительные особенности:
1. Если конструкция `(?imnsx)` указана без `:` и группы выражения, она применяется ко всему шаблону.
2. При наличии `:` параметры действуют только внутри группы.

#### Когда использовать каждый способ?

- **Через строку-шаблон**: удобно, если параметры очевидны и нужны только для конкретного шаблона.
- **Через `RegexOptions`**: полезно, если параметры задаются динамически в коде или требуется включить параметры, недоступные в строке (например, `RegexOptions.Compiled`).
- **Комбинация**: гибкий вариант для сложных сценариев, где нужно объединить преимущества обоих подходов.


### Примеры использования параметров

#### 1. Параметры по умолчанию {id="1_5"}
[По умолчанию](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#default-options) регулярные выражения учитывают регистр, пробелы значимы, а строки обрабатываются целиком.
```c#
string text = "Hello\nworld";
string pattern = @"world$";

bool isMatch = Regex.IsMatch(text, pattern);
Console.WriteLine(isMatch); // False, так как $ проверяет конец всей строки
```

```c#
Regex regex = new Regex("hello");
Console.WriteLine(regex.IsMatch("HELLO")); // False
```

#### 2. Сопоставление без учета регистра (`RegexOptions.IgnoreCase`) {id="2_5"}
[Позволяет игнорировать регистр символов](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#case-insensitive-matching).
```c#
string text = "Hello World";
string pattern = @"world";

bool isMatch = Regex.IsMatch(text, pattern, RegexOptions.IgnoreCase);
Console.WriteLine(isMatch); // True, регистр игнорируется
```

```c#
Regex regex = new Regex("hello", RegexOptions.IgnoreCase);
Console.WriteLine(regex.IsMatch("HELLO")); // True
```

#### 3. Многострочный режим (`RegexOptions.Multiline`) {id="3_2"}
[Позволяет механизму регулярных выражений обрабатывать входную строку, которая состоит из нескольких строк](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#multiline-mode).
`^` и `$` будут указывать на начало и конец каждой строки, а не всей строки.
```c#
string text = "Hello\nWorld";
string pattern = @"^World";

bool isMatch = Regex.IsMatch(text, pattern, RegexOptions.Multiline);
Console.WriteLine(isMatch); // True, ^ проверяет начало каждой строки
```

```c#
Regex regex = new Regex("^hello", RegexOptions.Multiline);
string input = "hello\nworld";
Console.WriteLine(regex.IsMatch(input)); // True
```

#### 4. Однострочный режим (`RegexOptions.Singleline`) {id="4_3"}
[Позволяет механизму регулярных выражений обрабатывать входную строку так, будто она состоит из одной строки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#single-line-mode).
`.` будет соответствовать любому символу, включая символы новой строки.
```c#
string text = "Hello\nWorld";
string pattern = @"Hello.World";

bool isMatch = Regex.IsMatch(text, pattern, RegexOptions.Singleline);
Console.WriteLine(isMatch); // True, точка соответствует символу новой строки
```

```c#
Regex regex = new Regex("hello.world", RegexOptions.Singleline);
string input = "hello\nworld";
Console.WriteLine(regex.IsMatch(input)); // True
```

#### 5. Только явные захваты (`RegexOptions.ExplicitCapture`) {id="5_2"}
[Захватываются только явно заданные группы](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#explicit-captures-only).
```c#
string text = "Hello";
string pattern = @"(?<word>Hello)";

var match = Regex.Match(text, pattern, RegexOptions.ExplicitCapture);
Console.WriteLine(match.Groups["word"].Value); // "Hello"
```

```c#
Regex regex = new Regex("(?<name>hello) world", RegexOptions.ExplicitCapture);
Console.WriteLine(regex.IsMatch("hello world")); // True
```

#### 6. Скомпилированные регулярные выражения (`RegexOptions.Compiled`) {id="6_2"}
[Позволяет скомпилировать регулярное выражение для повышения производительности](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#compiled-regular-expressions).
```c#
var regex = new Regex(@"\d+", RegexOptions.Compiled);
Console.WriteLine(regex.IsMatch("123")); // True
```
```c#
Regex regex = new Regex("hello", RegexOptions.Compiled);
Console.WriteLine(regex.IsMatch("hello")); // True
```

#### 7. Пропуск пробелов (`RegexOptions.IgnorePatternWhitespace`) {id="7_2"}
[Пробелы и комментарии игнорируются](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#ignore-white-space).
```c#
string pattern = @"
    \d+   # Числа
    [a-z]+ # Буквы";
string text = "123abc";

bool isMatch = Regex.IsMatch(text, pattern, RegexOptions.IgnorePatternWhitespace);
Console.WriteLine(isMatch); // True
```

```c#
Regex regex = new Regex(@"hello\s+world", RegexOptions.IgnorePatternWhitespace);
Console.WriteLine(regex.IsMatch("hello   world")); // True
```

#### 8. Режим "справа налево" (`RegexOptions.RightToLeft`) {id="8_2"}
[Поиск идет справа налево](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#right-to-left-mode).
```c#
string text = "123abc";
string pattern = @"\b[a-z]+";

var match = Regex.Match(text, pattern, RegexOptions.RightToLeft);
Console.WriteLine(match.Value); // "abc"
```

```c#
Regex regex = new Regex("world", RegexOptions.RightToLeft);
string input = "hello world";
Console.WriteLine(regex.IsMatch(input)); // True
```

#### 9. Поведение ECMAScript (`RegexOptions.ECMAScript`)
[Включает совместимость с ECMAScript](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#ecmascript-matching-behavior).
```c#
string text = "123";
string pattern = @"\d";

bool isMatch = Regex.IsMatch(text, pattern, RegexOptions.ECMAScript);
Console.WriteLine(isMatch); // True
```

```c#
Regex regex = new Regex(@"\d+", RegexOptions.ECMAScript);
Console.WriteLine(regex.IsMatch("123")); // True
```

#### 10. Сравнение с использованием инвариантного языка (`RegexOptions.CultureInvariant`) {id="10_2"}
[Игнорирует региональные настройки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#compare-using-the-invariant-culture).
```c#
string text = "straße";
string pattern = @"STRASSE";

bool isMatch = Regex.IsMatch(text, pattern, RegexOptions.IgnoreCase | RegexOptions.CultureInvariant);
Console.WriteLine(isMatch); // True
```

```c#
Regex regex = new Regex("ß", RegexOptions.CultureInvariant);
Console.WriteLine(regex.IsMatch("ss")); // False
```

#### 11. *Режим без обратного отслеживания (`RegexOptions.NonBacktracking`) 
[Гарантирует линейное время обработки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/regular-expression-options#nonbacktracking-mode). (только .NET 7 и выше)
```c#
string text = "abc";
string pattern = @"(a|b)c";

bool isMatch = Regex.IsMatch(text, pattern, RegexOptions.NonBacktracking);
Console.WriteLine(isMatch); // True
```
```c#
Regex regex = new Regex(".*", RegexOptions.NonBacktracking);
Console.WriteLine(regex.IsMatch("hello world")); // True
```

## Комментарии в регулярных выражениях

Регулярные выражения — это мощный инструмент для работы с текстом. Они помогают находить, заменять 
или проверять строки по определенным шаблонам. Но иногда шаблоны становятся длинными и сложными, 
и разобраться в них непросто. Тут на помощь приходят **другие конструкции**, такие как **комментарии**. 
Они делают регулярные выражения понятнее и помогают объяснить, что делает тот или иной кусок шаблона.

Комментарии позволяют описать, что делает каждая часть шаблона, не влияя на сам процесс сопоставления.

### Зачем нужны комментарии?
Представьте, что вы создали сложное регулярное выражение, которое проверяет номер телефона или почтовый индекс. Через неделю вы снова открываете его и не понимаете, как оно работает. Комментарии решают эту проблему: они помогают вам (или другому программисту) быстро вспомнить, зачем нужен каждый кусок шаблона.

### Типы комментариев в регулярных выражениях

В .NET поддерживаются два типа комментариев в регулярных выражениях:

1. **[Встроенные комментарии](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/miscellaneous-constructs-in-regular-expressions#inline-comment)** — пишутся прямо внутри регулярного выражения.
2. **[Комментарии в конце строки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/miscellaneous-constructs-in-regular-expressions#end-of-line-comment)** — добавляются после шаблона.

Разберем их подробнее с примерами.

### 1. Встроенные комментарии {id="1_6"}

Встроенные комментарии позволяют описывать отдельные части регулярного выражения. Они добавляются с помощью конструкции `(?#комментарий)`. Такой комментарий **не влияет на выполнение** регулярного выражения — это просто текст для пояснения.

#### Как это работает?
- Все, что находится внутри `(?# )`, считается комментарием.
- Этот комментарий может находиться в любом месте регулярного выражения.

#### Пример:
Регулярное выражение, которое ищет три буквы, за которыми следует пробел:
```c#
string pattern = @"\w{3}(?#Ищем три буквы)\s";
string input = "abc def ghi";
Regex regex = new Regex(pattern);
Console.WriteLine(regex.IsMatch(input)); // True
```

**Объяснение:**
- `\w{3}` — Ищет три символа (буквы, цифры или подчеркивания).
- `(?#Ищем три буквы)` — Комментарий для пояснения, что мы ищем.
- `\s` — Проверяет, есть ли пробел после этих символов.

Этот комментарий делает шаблон понятнее: даже через месяц вы вспомните, что здесь происходит.

### 2. Комментарии в конце строки {id="2_6"}

Комментарии в конце строки полезны, когда вы включаете в регулярное выражение флаг **`RegexOptions.IgnorePatternWhitespace`**. Этот флаг позволяет игнорировать пробелы и переносы строк в шаблоне, превращая их в читаемые блоки. Комментарии в конце строки пишутся после символа `#`.

#### Как это работает?
- Все, что идет после символа `#` до конца строки, считается комментарием.
- Для использования комментариев в конце строки обязательно включайте флаг `RegexOptions.IgnorePatternWhitespace`.

#### Пример:
Регулярное выражение, которое проверяет правильность электронной почты:
```c#
string pattern = @"
    ^\w+       # Логин: буквы, цифры или _
    @          # Символ @
    \w+\.\w+   # Доменное имя
";
Regex regex = new Regex(pattern, RegexOptions.IgnorePatternWhitespace);
string input = "user@example.com";
Console.WriteLine(regex.IsMatch(input)); // True
```

**Объяснение:**
- `^\w+` — Проверяет, что строка начинается с набора символов (логин).
- `@` — Проверяет наличие символа `@` в адресе.
- `\w+\.\w+` — Указывает, что после `@` идет доменное имя с точкой.

Комментарии после `#` объясняют, что делает каждая часть шаблона.

### Когда использовать комментарии?

- **При сложных выражениях**. Чем сложнее регулярное выражение, тем полезнее комментарии. Они экономят время при поддержке и исправлении кода.
- **Для работы в команде**. Комментарии помогают другим программистам понять ваш код.
- **Когда нужно разбить шаблон на части**. Вместо одной длинной строки вы можете записать регулярное выражение в несколько строк с пояснениями.

Комментарии в регулярных выражениях — это отличный способ сделать сложные шаблоны читаемыми и понятными. Встроенные комментарии помогают объяснить отдельные куски шаблона, а комментарии в конце строки делают весь шаблон более структурированным. Используйте их, чтобы сэкономить время и нервы как свои, так и ваших коллег!

## Объектная модель регулярных выражений

[Объектная модель регулярных выражений](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model) помогает легко находить, извлекать и обрабатывать текстовые данные.

### Механизм регулярных выражений

[Механизм регулярных выражений](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#the-regular-expression-engine) в .NET представлен классом `Regex`. Он отвечает за:

- Синтаксический анализ шаблона.
- Сопоставление шаблона с текстом.
- Выполнение операций, таких как поиск, замена или разбиение строк.

Вы можете использовать механизм двумя способами:
1. **Статические методы класса `Regex`**. Удобно для быстрого применения регулярных выражений.
2. **Создание экземпляра `Regex`**. Полезно, если вы работаете с одним шаблоном много раз.

#### Что можно делать с регулярными выражениями?
- [Сопоставление шаблона регулярного выражения](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#match-a-regular-expression-pattern).
- [Извлечение одного совпадения или первого совпадения](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#extract-a-single-match-or-the-first-match).
- [Извлечение всех совпадений](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#extract-all-matches).
- [Замена сопоставленной подстроки](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#replace-a-matched-substring).
- [Разделение одной строки на массив строк](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#split-a-single-string-into-an-array-of-strings).

Давайте рассмотрим каждую операцию с примерами.

#### Сопоставление шаблона регулярного выражения

Метод [Regex.IsMatch](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regex.ismatch) проверяет, соответствует ли строка заданному шаблону регулярного выражения. Если соответствует, он возвращает true, иначе — false. Этот метод обычно используют для проверки правильности формата строки.

**Пример:** проверим, содержит ли строка слово "школа".

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string input = "Сегодня мы идем в школу.";
        string pattern = @"школа";

        if (Regex.IsMatch(input, pattern))
        {
            Console.WriteLine("Строка содержит слово 'школа'.");
        }
        else
        {
            Console.WriteLine("Слово 'школа' не найдено.");
        }
    }
}
```

**Объяснение:**  
Метод `Regex.IsMatch` возвращает `true`, если строка соответствует шаблону.

**Пример:** Проверка номера социального страхования США.
```c#
string input = "123-45-6789";
string pattern = @"^\d{3}-\d{2}-\d{4}$";

if (Regex.IsMatch(input, pattern))
{
    Console.WriteLine("Номер социального страхования корректный.");
}
else
{
    Console.WriteLine("Номер социального страхования некорректный.");
}
```  
В этом примере проверяется, соответствует ли строка формату `XXX-XX-XXXX`, где `X` — цифра.

#### Извлечение одного совпадения или первого совпадения

Метод [Regex.Match](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regex.match) находит первое совпадение строки с шаблоном регулярного выражения и возвращает объект Match. Этот объект содержит информацию о совпадении, включая его текст и позицию. Если совпадение найдено (свойство Match.Success равно true), можно получить следующее совпадение, вызвав метод Match.NextMatch. Этот процесс продолжается до тех пор, пока совпадений не останется.

**Пример:** найдем первое слово, начинающееся с буквы "с".

```c#
string input = "Сегодня суббота, а завтра воскресенье.";
string pattern = @"\bс\w*";

Match match = Regex.Match(input, pattern);
if (match.Success)
{
    Console.WriteLine($"Найдено слово: {match.Value}");
}
```

**Объяснение:**
- `\b` указывает на границу слова.
- `с\w*` ищет слово, начинающееся с "с".

**Пример:** Поиск повторяющихся слов в строке.
```c#
string input = "The the cat cat sat sat on on the the mat.";
string pattern = @"\b(\w+)\s\1\b";

Match match = Regex.Match(input, pattern);

while (match.Success)
{
    Console.WriteLine($"Найдено совпадение: '{match.Value}' на позиции {match.Index}");
    match = match.NextMatch();
}
```  
В этом примере регулярное выражение `\b(\w+)\s\1\b` находит повторяющиеся слова, такие как "the the", "cat cat", и выводит их на экран.

#### Извлечение всех совпадений

Метод [Regex.Matches](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regex.matches) позволяет найти все совпадения строки с шаблоном регулярного выражения за один вызов. Он возвращает объект MatchCollection, который содержит информацию обо всех найденных совпадениях. Это упрощает работу, так как нет необходимости вручную вызывать NextMatch для поиска следующих совпадений.

**Пример:** найдем все слова, начинающиеся с "в".

```c#
string input = "Весна в воздухе, видны цветы.";
string pattern = @"\bв\w*";

MatchCollection matches = Regex.Matches(input, pattern);
foreach (Match match in matches)
{
    Console.WriteLine($"Найдено: {match.Value}");
}
```

**Объяснение:**  
Метод `Regex.Matches` возвращает коллекцию всех совпадений.

#### Замена сопоставленной подстроки

Метод [Regex.Replace](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regex.replace) заменяет все части строки, которые соответствуют шаблону регулярного выражения, на заданный текст или другой шаблон. После замены он возвращает изменённую строку.

**Пример:** заменим все цифры в строке на звездочки.

```c#
string input = "Мой номер: 123-456-789.";
string pattern = @"\d";
string replacement = "*";

string result = Regex.Replace(input, pattern, replacement);
Console.WriteLine(result); // Мой номер: ***-***-***.
```

**Объяснение:**  
`\d` означает любую цифру. Метод `Regex.Replace` заменяет все совпадения.

**Пример:** Добавление символа доллара перед числами.
```c#
string input = "Цены: 10, 20, 30.";
string pattern = @"\b\d+\b";
string replacement = "$$$&";

string result = Regex.Replace(input, pattern, replacement);
Console.WriteLine(result);
```
**Результат:**  
`Цены: $10, $20, $30.`

В этом примере каждая найденная цифра заменяется на ту же цифру, но с добавленным символом доллара перед ней.

#### Разделение одной строки на массив строк

Метод [Regex.Split](https://learn.microsoft.com/ru-ru/dotnet/api/system.text.regularexpressions.regex.split) разбивает входную строку на части, используя совпадения регулярного выражения как разделители. Результат — массив строк, который содержит части исходной строки.

**Пример:** разобьем предложение на слова.

```c#
string input = "Привет, как дела?";
string pattern = @"\s+";

string[] words = Regex.Split(input, pattern);
foreach (string word in words)
{
    Console.WriteLine(word);
}
```

**Объяснение:**  
`\s+` ищет один или несколько пробелов. Метод `Regex.Split` разделяет строку по этим пробелам.

**Пример:** Разделение строки с нумерованным списком.
```c#
string input = "1. Первый пункт 2. Второй пункт 3. Третий пункт";
string pattern = @"\d+\.\s";

string[] result = Regex.Split(input, pattern);
foreach (string part in result)
{
    if (!string.IsNullOrEmpty(part))
        Console.WriteLine(part);
}
```
**Результат:**
```
Первый пункт  
Второй пункт  
Третий пункт  
```  

В примере строка разделяется по шаблону чисел с точкой и пробелом, извлекая содержимое каждого пункта списка.

### Объекты MatchCollection и Match объекты

#### Класс MatchCollection

[MatchCollection](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#the-matchcollection-class) представляет собой список всех совпадений, найденных с помощью `Regex.Matches`.

**Пример:** найдем все гласные буквы в строке.

```c#
string input = "Программирование";
string pattern = @"[аеёиоуыэюя]";

MatchCollection matches = Regex.Matches(input, pattern);
foreach (Match match in matches)
{
    Console.WriteLine(match.Value);
}
```

**Объяснение:**
- `[аеёиоуыэюя]` задает множество гласных.
- Каждый элемент коллекции `MatchCollection` — это найденная буква.

#### Класс Match

Объект [Match](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#the-match-class) представляет одно совпадение. У него есть свойства, например:
- `Value` — найденный текст.
- `Index` — позиция совпадения.

**Пример:** определим, где в строке начинается слово "кот".

```c#
string input = "У кота котенок.";
string pattern = @"\bкот\b";

Match match = Regex.Match(input, pattern);
if (match.Success)
{
    Console.WriteLine($"Найдено: {match.Value} на позиции {match.Index}");
}
```

### Класс GroupCollection

[GroupCollection](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#the-groupcollection-class) содержит группы, которые выделяются в шаблоне с помощью скобок `()`.

**Пример:** найдем имя и фамилию в строке.

```c#
string input = "Иван Иванов";
string pattern = @"(\w+)\s+(\w+)";

Match match = Regex.Match(input, pattern);
if (match.Success)
{
    Console.WriteLine($"Имя: {match.Groups[1].Value}");
    Console.WriteLine($"Фамилия: {match.Groups[2].Value}");
}
```

**Объяснение:**
- Первая группа `(\w+)` — имя.
- Вторая группа `(\w+)` — фамилия.

### Захватываемая группа

[Захватываемая группа](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#the-captured-group) — это часть строки, которую выделяет регулярное выражение с использованием скобок `()`. Захватываемая группа позволяет извлечь отдельные части текста из строки.

**Пример:** Найдем дату в формате `ДД.ММ.ГГГГ` и разделим её на день, месяц и год.

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string input = "Сегодня 11.01.2025, а завтра 12.01.2025.";
        string pattern = @"(\d{2})\.(\d{2})\.(\d{4})";

        MatchCollection matches = Regex.Matches(input, pattern);
        foreach (Match match in matches)
        {
            Console.WriteLine($"Дата: {match.Value}");
            Console.WriteLine($"День: {match.Groups[1].Value}");
            Console.WriteLine($"Месяц: {match.Groups[2].Value}");
            Console.WriteLine($"Год: {match.Groups[3].Value}");
        }
    }
}
```

**Объяснение:**
1. `(\d{2})` — первая группа, выделяет день.
2. `(\d{2})` — вторая группа, выделяет месяц.
3. `(\d{4})` — третья группа, выделяет год.

**Результат:**
```
Дата: 11.01.2025
День: 11
Месяц: 01
Год: 2025
Дата: 12.01.2025
День: 12
Месяц: 01
Год: 2025
```

### Класс CaptureCollection

[CaptureCollection](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#the-capturecollection-class) хранит все совпадения внутри одной группы.

**Пример:** найдем все повторения слова "кот".

```c#
string input = "кот кот котенок";
string pattern = @"(кот)+";

Match match = Regex.Match(input, pattern);
if (match.Success)
{
    foreach (Capture capture in match.Groups[1].Captures)
    {
        Console.WriteLine(capture.Value);
    }
}
```

### Класс Capture

Класс [Capture](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/the-regular-expression-object-model#the-capture-class) предоставляет информацию о захваченных данных. Он используется внутри `CaptureCollection` для работы с частями текста, которые были захвачены группами. Он особенно полезен, когда группа захватывает несколько подстрок.

**Пример:** Найдем все вхождения числа в строке с повторением.

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string input = "123 456 123 789";
        string pattern = @"(123)+";

        Match match = Regex.Match(input, pattern);
        if (match.Success)
        {
            Console.WriteLine($"Полное совпадение: {match.Value}");
            
            // Вывод всех захваченных частей
            foreach (Capture capture in match.Groups[1].Captures)
            {
                Console.WriteLine($"Захвачено: {capture.Value} на позиции {capture.Index}");
            }
        }
    }
}
```

**Объяснение:**
1. `123` — это часть текста, которая повторяется.
2. `(123)+` — группа захватывает повторяющиеся подстроки.

**Результат:**
```
Полное совпадение: 123123
Захвачено: 123 на позиции 0
Захвачено: 123 на позиции 3
```

**Итог:**
- Захватываемая группа позволяет извлекать части строки.
- Класс `Capture` дает доступ к каждой части текста, захваченной в группе.

## Поведение и производительность регулярных выражений в .NET {id="net_2"}

Регулярные выражения — это мощный инструмент для работы со строками. Они используются для поиска, проверки, разделения и замены текста. 
[В .NET обработка регулярных выражений имеет свои особенности](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/details-of-regular-expression-behavior), благодаря чему они быстрые, гибкие и поддерживают широкий набор функций. Давайте разберемся, как работает механизм регулярных выражений в .NET, что такое NFA-машины, и рассмотрим возможности обработчика .NET.

### Преимущества NFA-машин

#### Что такое NFA- и DFA-машины?

NFA (недетерминированный конечный автомат) и DFA (детерминированный конечный автомат) — это два типа моделей, которые используются для обработки регулярных выражений.

- **DFA (детерминированный конечный автомат)**:  
  У DFA есть четкие правила, которые определяют, куда двигаться на каждом этапе. Машина в любой момент знает точно, в каком состоянии она находится. DFA работает быстро, но может быть сложной в реализации для более сложных регулярных выражений.

- **NFA (недетерминированный конечный автомат)**:  
  У NFA нет строгих правил, куда двигаться дальше. Она пытается испльзовать множество возможных вариантов одновременно и выбирает тот, который приводит к успешному совпадению. Это позволяет обрабатывать сложные шаблоны, но при большом количестве вариантов NFA может быть медленнее.

#### Разница между NFA и DFA {id="nfa-dfa_1"}

- **DFA**:
    + Быстрая обработка.
    + Ограниченные возможности.
    + Четко определенный путь обработки.

- **NFA**:
    + Поддержка сложных выражений.
    + Может "подбирать" шаблон разными способами.
    + Гибче, чем DFA.

#### Почему NFA-машины эффективны в .NET

[Механизм регулярных выражений в .NET использует NFA, что дает следующие преимущества](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/details-of-regular-expression-behavior#benefits-of-the-nfa-engine):

1. **Гибкость**: NFA поддерживает ленивые квантификаторы, положительный/отрицательный поиск и другие сложные конструкции.
2. **Компактность**: NFA может обрабатывать даже сложные шаблоны, которые не поддерживаются DFA.
3. **Поддержка сложных выражений**: Например, выражения с условными оценками или сбалансированными группами.

### Возможности обработчика .NET {id="net_1"}

[Обработчик регулярных выражений в .NET](https://learn.microsoft.com/ru-ru/dotnet/standard/base-types/details-of-regular-expression-behavior#net-engine-capabilities) поддерживает множество функций, которые делают работу с шаблонами более гибкой. Вот основные возможности с примерами.

#### Ленивые квантификаторы

Обычно квантификаторы, такие как `*`, `+`, `{n,m}`, захватывают максимально возможное количество символов. Ленивые квантификаторы (`*?`, `+?`, `{n,m}?`) делают то же самое, но с минимальным количеством символов.

**Пример:**
```c#
string text = "abcabc";
string pattern = "a.*?c"; // Ленивый квантификатор *?
Match match = Regex.Match(text, pattern);
Console.WriteLine(match.Value); // Вывод: "abc"
```

#### Положительный поиск вперед: `(?=...)`

Позволяет искать часть строки, которая следует за определенным шаблоном, но сам шаблон не включается в результат.

**Пример:**
```c#
string text = "abc123def";
string pattern = @"\d+(?=def)"; // Число перед "def"
Match match = Regex.Match(text, pattern);
Console.WriteLine(match.Value); // Вывод: "123"
```

#### Отрицательный поиск вперед: `(?!...)`

Находит строку, если за ней **не** следует указанное выражение.

**Пример:**
```c#
string text = "abc123xyz";
string pattern = @"\d+(?!xyz)"; // Число не перед "xyz"
Match match = Regex.Match(text, pattern);
Console.WriteLine(match.Success); // Вывод: False
```

#### Условная оценка: `(?...)`

Позволяет проверять условие внутри регулярного выражения.

**Пример:**
```c#
string pattern = @"(?(?=\d)\d{3}-\d{2}-\d{4}|[A-Z]{5})";
Console.WriteLine(Regex.IsMatch("123-45-6789", pattern)); // True
Console.WriteLine(Regex.IsMatch("ABCDE", pattern)); // True
```

#### Сбалансированные группы: `(?<имя1-имя2>...)`

Используются для обработки вложенных конструкций, таких как скобки или HTML-теги.

**Пример:**
```c#
string text = "((a+b)*c)";
string pattern = @"(?<Open>\()|(?<-Open>\))";
MatchCollection matches = Regex.Matches(text, pattern);
int balance = 0;
foreach (Match match in matches)
{
    if (match.Groups["Open"].Success) balance++;
    if (match.Groups["Open"].Success) balance--;
}
Console.WriteLine(balance == 0 ? "Сбалансировано" : "Несбалансировано");
```

#### Атомарные группы: `(?>...)`

Позволяют создавать группы, которые не будут пересматривать свои совпадения, чтобы ускорить обработку.

**Пример:**
```c#
string text = "aaaab";
string pattern = @"a(?>aa)a";
Console.WriteLine(Regex.IsMatch(text, pattern)); // False
```

#### Поиск справа налево

Обработка строки в обратном направлении.

**Пример:**
```c#
string text = "abc123def";
string pattern = @"\d+";
Regex regex = new Regex(pattern, RegexOptions.RightToLeft);
Match match = regex.Match(text);
Console.WriteLine(match.Value); // Вывод: "123"
```

#### Положительный поиск назад: `(?<=...)`

Ищет совпадение, которое **предшествует** указанному шаблону.

**Пример:**
```c#
string text = "abc123def";
string pattern = @"(?<=abc)\d+"; // Число после "abc"
Match match = Regex.Match(text, pattern);
Console.WriteLine(match.Value); // Вывод: "123"
```

#### Отрицательный поиск назад: `(?<!...)`

Ищет совпадение, которое **не предшествует** указанному шаблону.

**Пример:**
```c#
string text = "123abc";
string pattern = @"(?<!abc)\d+"; // Число не после "abc"
Match match = Regex.Match(text, pattern);
Console.WriteLine(match.Success); // Вывод: False
```

### Заключение

Механизм регулярных выражений в .NET построен на базе NFA, что дает гибкость и поддержку сложных шаблонов. Благодаря множеству возможностей, таких как ленивые квантификаторы, условные выражения и поиск назад, вы можете создавать мощные и эффективные шаблоны для работы с текстом.

## Примеры

### 5.1 Поиск ссылок

```c#
string pattern = @"href\s*=\s*""([^""]*)""";
```

#### Объяснение:
Это регулярное выражение используется для поиска ссылок, которые определяются в HTML-тегах, например, в тегах `<a>`.

- **`href`**: Ищем буквально строку `"href"`, которая указывает на атрибут ссылки в HTML.
- **`\s*`**: Это обозначает **ноль или более пробельных символов** (включая пробелы, табуляции и т.д.). Он нужен для того, чтобы учесть возможные пробелы между атрибутом `href` и знаком равенства `=`.
- **`=`**: Ищем символ **равно**. Это стандартный разделитель между атрибутом и его значением в HTML.
- **`\s*`**: Снова разрешаем ноль или более пробельных символов после знака равенства.
- **`""`**: Ожидаем, что значение атрибута будет заключено в **двойные кавычки**.
- **`([^""]*)`**: Это самая важная часть выражения.
    - **`[^""]`**: Это **отрицательное соответствие**, которое говорит, что мы ищем любой символ, кроме двойной кавычки. Это важно, чтобы остановить захват при встрече с завершающей кавычкой.
    - **`*`**: Квантификатор, который означает "повторить ноль или более раз". Это позволяет захватывать весь текст между кавычками (например, URL).
    - Таким образом, эта часть выражения захватывает **содержимое** атрибута `href`, т.е. саму ссылку (URL).

#### Пример:
Для строки:
```html
<a href="https://example.com">Click here</a>
```

Это регулярное выражение найдет `"https://example.com"` как значение атрибута `href`.

### 5.2 Форматы даты

```c#
string pattern = @"(\d{2})-(\d{2})-(\d{4})";
```

#### Объяснение:
Это регулярное выражение используется для поиска дат в формате **день-месяц-год**. Например, для даты вида `31-12-2023`.

- **`\d{2}`**: Это выражение ищет **две цифры** подряд.
    - **`\d`** — соответствует любой цифре от 0 до 9.
    - **`{2}`** — указывает, что должно быть именно две цифры.
      Таким образом, **`(\d{2})`** захватывает день, например, `31`.

- **`-`**: Ищем **дефис** между днями, месяцами и годами.

- **`\d{2}`**: Ищем еще одну пару цифр, которая будет представлять месяц, например, `12`.

- **`-`**: Еще один дефис.

- **`\d{4}`**: Ищем **четыре цифры**, которые представляют год, например, `2023`.

#### Пример:
Для строки:
```text
31-12-2023
```

Это регулярное выражение найдет:
- День: `31`
- Месяц: `12`
- Год: `2023`

#### Важное замечание:
Это регулярное выражение не проверяет, является ли дата **действительной** (например, 31 февраля будет найдено так же, как и 28 февраля). Чтобы учитывать такие проверки, необходимо использовать более сложные шаблоны или дополнительные проверки в коде.

### 5.3 Проверка IP-адресов

**Задача**: Определить правильность IPv4-адреса.  
IPv4-адрес состоит из четырёх чисел от 0 до 255, разделённых точками. Для поиска такого шаблона мы можем использовать регулярное выражение.

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // IPv4-адреса для проверки
        string[] ipAddresses = {
            "192.168.1.1",    // корректный
            "255.255.255.255", // корректный
            "256.300.1.1",    // некорректный
            "127.0.0.1",      // корректный
            "192.168.0",      // некорректный
            "192.168.-1.1"    // некорректный
        };

        // Оптимизированный шаблон для проверки IPv4-адресов
        string ipv4Pattern = @"^((25[0-5]|2[0-4][0-9]|[0-1]?[0-9][0-9]?)\.){3}"
                           + @"(25[0-5]|2[0-4][0-9]|[0-1]?[0-9][0-9]?)$";

        // Проверка и вывод только корректных адресов
        foreach (string ip in ipAddresses)
        {
            if (Regex.IsMatch(ip, ipv4Pattern))
            {
                Console.WriteLine($"Корректный IP-адрес: {ip}");
            }
            else
            {
                Console.WriteLine($"Некорректный IP-адрес: {ip}");
            }
        }
    }
}
```

### Объяснение шаблона
1. **Группировка:**  
   Мы выделили проверку для одного октета (`25[0-5]|2[0-4][0-9]|[0-1]?[0-9][0-9]?`) в группу.

2. **Квантификатор `{3}`:**  
   Использован квантификатор `{3}` для указания, что часть `(25[0-5]|2[0-4][0-9]|[0-1]?[0-9][0-9]?)\.` должна повторяться ровно три раза. Это покрывает три первых октета, за которыми идет точка.

3. **Финальная группа:**  
   Последний октет (`25[0-5]|2[0-4][0-9]|[0-1]?[0-9][0-9]?`) добавлен отдельно, так как после него точка не требуется.

4. **Начало (`^`) и конец (`$`):**  
   Эти символы гарантируют, что вся строка должна соответствовать шаблону, а не только её часть.

### Преимущества этого подхода:
- **Меньше повторений:** Проверка октета вынесена в группу и переиспользуется.
- **Читаемость:** Шаблон стал короче и понятнее.
- **Меньше ошибок:** Сокращение повторений снижает вероятность ошибок при изменении шаблона.

Этот шаблон проверяет корректность IPv4-адреса и удобен для понимания и поддержки.

### 5.4 Поиск телефонных номеров

**Задача**: Найти номера телефонов в формате `+7 (XXX) XXX-XX-XX`.

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string text = "Контакты: +7 (495) 123-45-67, +7 (812) 765-43-21.";
        string pattern = @"\+7\s\(\d{3}\)\s\d{3}-\d{2}-\d{2}";

        MatchCollection matches = Regex.Matches(text, pattern);
        foreach (Match match in matches)
        {
            Console.WriteLine($"Телефон: {match.Value}");
        }
    }
}
```

**Объяснение**:
- Шаблон `@"\+7\s\(\d{3}\)\s\d{3}-\d{2}-\d{2}"` находит номера в указанном формате.
- `\+7` соответствует префиксу номера.
- `\(\d{3}\)` — трёхзначный код региона в скобках.

### 5.5 Поиск HTML-тегов

**Задача**: Найти все HTML-теги в тексте.

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string html = "<div><h1>Заголовок</h1><p>Параграф</p></div>";
        string pattern = @"<[^>]+>";

        MatchCollection matches = Regex.Matches(html, pattern);
        foreach (Match match in matches)
        {
            Console.WriteLine($"Найден тег: {match.Value}");
        }
    }
}
```

**Объяснение**:
- Шаблон `@"<[^>]+>"` ищет строки, которые начинаются с `<`, содержат любые символы, кроме `>`, и заканчиваются на `>`.

### 5.6 Проверка пароля на сложность

**Задача**: Проверить, соответствует ли пароль требованиям (длина от 8 символов, содержит буквы, цифры и спецсимволы).

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string password = "P@ssw0rd123";
        string pattern = @"^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$";

        bool isValid = Regex.IsMatch(password, pattern);
        Console.WriteLine(isValid ? "Пароль соответствует требованиям" : "Пароль не соответствует требованиям");
    }
}
```

**Объяснение**:
- `^(?=.*[a-z])` — минимум одна строчная буква.
- `(?=.*[A-Z])` — минимум одна заглавная буква.
- `(?=.*\d)` — минимум одна цифра.
- `(?=.*[@$!%*?&])` — минимум один специальный символ.
- `{8,}` — длина пароля минимум 8 символов.

### 5.7 Замена номеров кредитных карт на маскированные значения

**Задача**: Замаскировать все номера кредитных карт, кроме последних четырёх цифр.

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string text = "Карты: 1234-5678-9012-3456, 9876-5432-1098-7654.";
        string pattern = @"\b\d{4}-\d{4}-\d{4}-(\d{4})\b";

        string result = Regex.Replace(text, pattern, "****-****-****-$1");
        Console.WriteLine(result);
    }
}
```

**Объяснение**:
- Шаблон `@"\b\d{4}-\d{4}-\d{4}-(\d{4})\b"` находит номера в формате "XXXX-XXXX-XXXX-XXXX".
- `$1` в строке замены вставляет последние четыре цифры.

### 5.8 Удаление всех символов, кроме букв и цифр

**Задача**: Очистить текст от всех символов, кроме букв и цифр.

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string text = "Текст с символами: !@#$%^&*()123.";
        string pattern = @"[^a-zA-Zа-яА-Я0-9]+";

        string result = Regex.Replace(text, pattern, "");
        Console.WriteLine(result); // "Текстссимволами123"
    }
}
```

**Объяснение**:
- Шаблон `@"[^a-zA-Zа-яА-Я0-9]+"` находит все символы, кроме букв и цифр.
- `Regex.Replace` удаляет найденные символы.

### 5.9 Извлечение хэштегов из текста

**Задача**: Найти все хэштеги в тексте.

```c#
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string text = "Популярные теги: #c#, #regex, #programming.";
        string pattern = @"#\w+";

        MatchCollection matches = Regex.Matches(text, pattern);
        foreach (Match match in matches)
        {
            Console.WriteLine($"Найден хэштег: {match.Value}");
        }
    }
}
```

**Объяснение**:
- Шаблон `"#\w+"` ищет строки, начинающиеся с `#`, за которыми следует одна или более буква или цифра.

Эти примеры охватывают самые популярные задачи с регулярными выражениями в C#. 