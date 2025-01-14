# Переменные в C#

Переменная — это именованная область памяти, используемая для хранения данных, которые могут изменяться во время 
выполнения программы. Она имеет тип, который определяет, какие данные можно хранить в переменной, и как они будут обрабатываться.

Напомню, что в C# есть две категории [типов](GrammarAndTerminologyCSharp.md#Types): [типы значений](GrammarAndTerminologyCSharp.md#ValueTypes) и [ссылочные типы](GrammarAndTerminologyCSharp.md#ReferenceTypes).
Соответственно и типы переменных так же относятся к этим двум категориям.

Переменные программы хранятся в оперативной памяти компьютера, которая выделяется программе операционной системой.

В зависимости от [категории типа](GrammarAndTerminologyCSharp.md#TypeDiff), переменные хранятся в разных областях памяти:
стеке или куче. Поэтому имеют свои особенности обработки.

На основе базовых типов существующих в .NET, вы можете создавать свои типы. И соответственно создавать переменные этих типов.

Как уже было сказано в определение переменные на то и переменные, что их значение может меняться во время выполнения программы
или они даже могут быть удалены из памяти, например сборщиком мусора, если они уже не нужны для выполнения программы.

Естественно, что по завершении работы программы все переменные которые она использовала так же удаляются из памяти.

Переменные могут получать свои значения не посредственно в ходе выполнения программы из пользовательского ввода, читаться из
файлов или баз данных, а так же быть на прямую заданы в коде программы.

Значения переменных так же могут выводиться на экран, принтер, файл, базу данных, отправляться по сети и т.п.

Каждая переменная имеет **тип**, **имя** и **значение (данные)**.

Например:
```C#
int price = 100;
```
В данном случае `int` - это тип переменной, `price` - это имя переменной, а `100` - это значение переменной. 

Рассматривайте переменную как ящик куда можно что-то поместить, вынуть и поместить что-то другое. Но поскольку C# строго
типизированный язык в определенные ящики, можно помещать только определенные типы данных.

Разные типы данных имеют разные размеры поэтому для них выделяются разные по размеру ящики. То есть для хранения переменных
разных типов в памяти компьютера выделяется различное количество бит.

В приведенном выше примере для переменной типа `int` в памяти выделяется 32 бита, что равно 4 байтам. Переменные типа `int` могут
содержать значения от -2,147,483,648 до 2,147,483,647.

А вот пример переменой типа `byte`:
```C#
byte ascii_symbol = 108;
```
Для переменной типа `byte` выделяется 8 бит, что рано 1 байту. Переменные типа `byte` могут содержать значения от 0 до 255.

## Представление информации в памяти компьютера

> Этот раздел желательно изучить и понять. Если сложно, то сделайте это в несколько заходов. Кроме того, в сети, много видео
> на это тему. Найдите и посмотрите их. Если не сразу всё поняли, то не страшно. Со временем просветление придёт.
> {style="note"}

Память измеряется в байтах. Один байт содержит 8 бит. 

**Что такое бит и байт?**
- **Бит** — это минимальная единица информации в компьютере, которая может принимать два значения: **0** или **1**.
- **Байт** — это последовательность из 8 бит. Он является стандартной минимальной единицей хранения данных в памяти компьютера.

**Как представляется информация в памяти компьютера?**

Компьютерная память устроена как огромный набор ячеек, каждая из которых может содержать 1 байт. В каждом байте 
хранятся 8 бит, которые могут быть **0** или **1**. Эти комбинации кодируют числа, символы, инструкции и другие данные 
с помощью кодировок (например, ASCII или Unicode для текста).

**Почему 1 байт может представлять 256 значений?**

Каждый бит в байте может быть либо **0**, либо **1**. Количество возможных комбинаций из 8 бит вычисляется как:  

$2^8 = 256$  

Таким образом, байт может представлять числа от **0 до 255** (если без знака) или от **-128 до 127** (если используется знак).  
Пример:
- `00000000` (все биты = 0) — это 0.
- `11111111` (все биты = 1) — это 255.

**Перевод из двоичной в десятичную**

Возьмем число **1011** (двоичное).  
Каждая цифра двоичного числа, в зависимости от своего положения (начиная справа), имеет вес, равный степени двойки, начиная с нуля:

| Вес цифры  | Цифра | Степень двойки | Значение |
|------------|-------|----------------|----------|
| 3 (слева)  | 1     | $2^3 = 8$      | 8        |
| 2          | 0     | $2^2 = 4$      | 0 (потому что 0 × 4 = 0) |
| 1          | 1     | $2^1 = 2$      | 2        |
| 0 (справа) | 1     | $2^0 = 1$      | 1        |

Теперь складываем только значения, которые **не равны 0**:  
$8 + 0 + 2 + 1 = 11$

**Результат:** $1011_2 = 11_{10}$

**Почему пропадает "4" в примере?**

В двоичной системе каждая **0** означает, что значение этой степени двойки не используется.  
В примере $1011_2$, цифра **0** на позиции $2^2$ даёт $0 * 4 = 0$, поэтому $4$ не добавляется в сумму.

**Перевод из десятичной в двоичную**

Возьмем число **13** (десятичное) и разделим целочисленным делением на 2, чтобы получить остатки:

1. **$13 \div 2 = 6$**, остаток **$1$**.
2. **$6 \div 2 = 3$**, остаток **$0$**.
3. **$3 \div 2 = 1$**, остаток **$1$**.
4. **$1 \div 2 = 0$**, остаток **$1$**.

Теперь записываем остатки **снизу вверх**:  
$1\ 1\ 0\ 1$

**Результат:** $13_{10} = 1101_2$


**Что такое целочисленное деление с остатком?**

В **целочисленном делении** результатом является только **целая часть** от деления, а остаток — это то, что "остается", 
если делимое не делится нацело.

Формула:  
$$
Делимое = (Делитель \times ЦелаяЧасть) + Остаток
$$

При этом:
- Остаток всегда меньше делителя.

Разберем $ 1 ÷ 2$ в контексте целочисленного деления с остатком:
1. Сколько раз $2$ помещается в $1$ без превышения? Ответ: $0$ раз (**целая часть = 0**).
2. Что осталось после этого? Осталось всё исходное число $1$, потому что $2$ в $1$ "не помещается".

Результат:  

$1 ÷  2 = 0 \, (\text{целая часть}) \, \text{и остаток 1}$.

**Объяснение целочисленного деления через раздачу пирогов:**

1. У тебя есть **13 пирогов**, ты раздаёшь их **группами по 2 пирога**. Раздавать можно только **целые** пироги. Резать пироги нельзя.
2. На каждом шаге:
    - Считаем, сколько раз можно раздать **по 2 целых пирога** (**целая часть деления**).
    - Считаем, сколько пирогов осталось (**остаток**).

**Шаги деления $13 \div 2$:**
1. **Первый шаг:**
    - У тебя есть $13$ пирогов. Сколько раз можно раздать по $2$ пирога?  
      $13 \div 2 = 6$ (**целая часть = 6**).
    - После раздачи $6 \times 2 = 12$ пирогов у тебя остался **1 пирог** (**остаток = 1**).

2. **Второй шаг:**
    - Теперь $6$ пирогов сколько раз можно раздать по $2$ пирога?  
      $6 \div 2 = 3$ (**целая часть = 3**).
    - После раздачи $3 \times 2 = 6$ пирогов осталось **0 пирогов** (**остаток = 0**).

3. **Третий шаг:**
    - Теперь  $3$ пирога сколько раз можно раздать по $2$?  
      $3 \div 2 = 1$ (**целая часть = 1**).
    - После раздачи $1 \times 2 = 2$ пирогов остался **1 пирог** (**остаток = 1**).

4. **Четвёртый шаг:**
    - И так остался $1$ пирог. Сколько раз можно раздать по $2$?  
      $1 \div 2 = 0$ (**целая часть = 0**). $0$ пирогов вы можете раздать. Поэтому у вас остается **1 пирог** (**остаток = 1**).
    - После раздачи $0 \times 2 = 0$ пирогов остался **1 пирог** (**остаток = 1**).

**Как собрать двоичное число:**
Остатки, которые мы получили (1, 0, 1, 1), записываем **снизу вверх**:  

$13_{10} = 1101_2$

**Кратко что мы проделали:**
1. На каждом шаге ты раздаёшь пироги **по 2 штуки за раз**.
2. Что остаётся после раздачи — это **остаток**, который записывается как разряд двоичного числа.
3. Процесс продолжается, пока у тебя не закончатся пироги (целая часть не станет 0).

### Представление отрицательных целых чисел в двоичной системе

Если двоичное число интерпретируется как знаковое, то старший бит (самый левый) указывает 
на знак числа:
- `0` — положительное число.
- `1` — отрицательное число.

**Общие шаги перевода отрицательного числа в двоичную систему**

1. **Найти двоичное представление положительного аналога числа.**
   - Например, для `-60` сначала возьмем `60`.

2. **Дополнить двоичное представление до разрядности типа.**
   - Например, если используем 8 бит, то записываем число в формате `0011_1100`.

3. **Инвертировать биты (заменить 1 на 0 и 0 на 1).**

4. **Добавить 1 к результату.**

### Пример: перевод числа `-60` в двоичную систему для 8-битного представления

1. **Положительный аналог числа:**
   - Число `60` в двоичной системе:
     ```
     60 (десятичное) = 0011_1100 (двоичное).
     ```

2. **Инверсия всех битов:**
   - Инвертируем (заменяем 1 на 0 и 0 на 1):
     ```
     0011_1100 → 1100_0011.
     ```

3. **Добавление 1:**
   - Прибавляем 1 к результату:
     ```
     1100_0011 + 1 = 1100_0100.
     ```

4. **Результат:**
   - Число `-60` в дополнительном коде для 8 бит:
     ```
     -60 = 1100_0100.
     ```

### Пример: перевод из двоичной системы обратно в десятичную: пример с `1100_0100`

1. **Проверить знак числа:**
   - Если старший бит равен 1 (в данном случае `1`), то число отрицательное.

2. **Инвертировать все биты:**
   - Инвертируем:
     ```
     1100_0100 → 0011_1011.
     ```

3. **Вычесть 1:**
   - Вычитаем 1:
     ```
     0011_1011 - 1 = 0011_1100.
     ```

4. **Перевести в десятичное:**
   - Число `0011_1100` в десятичной системе:
     ```
     0011_1100 = 60.
     ```

5. **Добавить знак:**
   - Так как старший бит изначально был 1, результат:
     ```
     -60.
     ```

Когда самый старший бит числа интерпретируется как знак числа, такое представление называют **дополнительным кодом** или
**Two's Complement**.

### Представление вещественных чисел
**Вещественное число** — это число с дробной частью, например: 42.021, 3.14 или -0.5. Такие числа нужны для точных расчетов, 
например, в физике или инженерии.

Поскольку числа в компьютере хранятся в двоичной системе (в виде 0 и 1). Для вещественных чисел используется специальный 
стандарт хранения — **IEEE 754**. Этот стандарт описывает, как представить вещественное число в виде трех частей:

### 1. **Знак** (1 бит): {id="1-1_1"}
- Если число положительное, бит равен 0.
- Если число отрицательное, бит равен 1.

### 2. **Порядок** (8 бит для float, 11 бит для double):
- Это смещение, которое показывает, на сколько разрядов нужно сдвинуть десятичную (а точнее, двоичную) точку.
- Порядок хранится с добавлением **смещения (bias)**:
    - Для `float` смещение = 127.
    - Для `double` смещение = 1023.

### 3. **Мантисса** (23 бита для float, 52 бита для double):
- Мантисса хранит значимые разряды числа, записанные в двоичном виде. Число всегда **нормализуется** так, чтобы первый разряд был равен 1 (**он не хранится явно, называется скрытым битом**).

### Для чего нужно смещение (bias)?
Смещение позволяет записывать как положительные, так и отрицательные значения экспоненты без дополнительных битов на знак:
- Если экспонента равна $E$, то в памяти хранится $E + bias$.
- Например, для `float`, если $E = -1$, то хранится $127 + (-1) = 126$.

#### Почему bias = 127 для float?
Смещение выбирается как половина диапазона экспоненты. Для 8 бит:
- Диапазон $[0, 255$, следовательно, bias = $127$.

Для `double` (11 бит):
- Диапазон $[0, 2047]$, следовательно, bias = $1023$.

### Аналогия для лучшего понимания bias {id="bias_1"}
Представьте, что вам нужно записывать как положительные, так и отрицательные числа, но вы можете использовать 
только положительные числа. Например:
- У вас есть диапазон чисел от $-50$ до $+50$.
- Вы добавляете $+50$ ко всем числам, чтобы диапазон стал $0$ до $100$.
    - $+50$ превращается в $100$,
    - $0$ превращается в $50$,
    - $-50$ превращается в $0$.

Точно так же добавляется смещение $+127$ для хранения истинного порядка в положительном виде.

### Что такое нормализованное число?
**Нормализованное число** — это такое представление числа, при котором его значимая часть записывается в виде числа, 
начинающегося с $1,$ (единица с запятой) и умножается на степень числа $2$. Это удобно, потому что все числа в 
таком формате имеют одинаковую структуру, что упрощает их хранение и обработку в компьютере.

Давайте разберем это на простом примере с числом $42,02$.

### 1. Число в десятичной системе: {id="1_2"}
Число $42,021$ — это обычное число, записанное в привычном десятичном формате.

Теперь переведем его в двоичную систему.

### 2. Преобразование числа в двоичную систему: {id="2_2"}
В двоичной системе это число будет выглядеть так:  
$
42,021_{10} = 101010.000001_2
$

**Расшифруем:**
- **Целая часть $42_{10}$** в двоичной системе это $101010_2$
- **Дробная часть $0,021_{10}$** в двоичной системе это примерно $0.000001_2$

Итак, $42,021_{10}$ в двоичной системе выглядит как $101010.000001_2$

### 3. Приведение к нормализованному виду: {id="3_3"}
Теперь нужно записать это число так, чтобы значимая часть числа начиналась с $1,$ а оставшуюся часть числа мы умножим 
на степень числа $2$.

#### Шаги:
1. **Переместим двоичную точку (запятую):**  
   Двигаем запятую так, чтобы перед ней осталась только одна $1$.  
   $$
   101010.000001_2 \rightarrow 1.01010000001_2
   $$
   (Мы сдвинули точку на 5 позиций влево. Это и будет степенью двойки)

2. **Запишем степень двойки:**  
   Чтобы вернуть число в исходное состояние, нужно умножить его на $2^5$, так как мы сдвинули точку на 5 позиций влево.

**Итоговое нормализованное представление:**  
$$
42,021_{10} = 1.01010000001_2 \times 2^5.
$$

### Зачем такие сложности?
- **Экономия места:** В нормализованном виде в памяти хранится только значимая часть (мантисса) и степень (порядок). Это позволяет не тратить место на незначащие нули.
- **Унификация:** Все числа представлены одинаково, что упрощает операции над ними (сложение, умножение и т.д.).

### Пояснение более простыми словами:
Представь, падаван, что у тебя есть число $42,021$, записанное в виде $101010.000001$ в двоичной системе. Чтобы сделать 
его удобным для хранения, мы «передвигаем» точку (запятую) так, чтобы число начиналось с $1$. Мы как будто говорим:
- "Возьмём $1.01010000001$, но чтобы вернуть точку назад на место, нужно умножить это число на $2^5$."

Так мы получаем **нормализованное представление** числа:  
$$
1.01010000001_2 \times 2^5.
$$

### Подробный пошаговый пример преобразования числа 42,021 в двоичное представление

Для преобразования числа $42,021$ в формат IEEE 754 (32-битное представление с плавающей точкой, или **float**), 
нам нужно выполнить несколько шагов. Включая преобразование целой и дробной части в двоичное представление, нормализацию, 
а также кодирование в соответствии с стандартом IEEE 754.

Давайте разберем это шаг за шагом, подробно объяснив, как это работает.

### Шаг 1: Представление числа в двоичной системе {id="1_3"}

#### 1.1. Целая часть {id="1-1_2"}
Целая часть числа — это $42$. Преобразуем её в двоичную систему, деля на 2 и записывая остатки:

$$
42 \div 2 = 21 \, \text{(остаток 0)}
$$
$$
21 \div 2 = 10 \, \text{(остаток 1)}
$$
$$
10 \div 2 = 5 \, \text{(остаток 0)}
$$
$$
5 \div 2 = 2 \, \text{(остаток 1)}
$$
$$
2 \div 2 = 1 \, \text{(остаток 0)}
$$
$$
1 \div 2 = 0 \, \text{(остаток 1)}
$$

Теперь читаем остатки снизу вверх:

$$
42_{10} = 101010_2
$$

#### 1.2. Дробная часть
Дробная часть — это $0,021$. Чтобы перевести её в двоичную систему, умножаем её на 2 и записываем целую часть каждого 
результата. Повторяем процесс, пока дробь не станет равной 0 (или пока точность не станет достаточной).

$$
0,021 \times 2 = 0,042 \quad (\text{целая часть } 0)
$$
$$
0,042 \times 2 = 0,084 \quad (\text{целая часть } 0)
$$
$$
0,084 \times 2 = 0,168 \quad (\text{целая часть } 0)
$$
$$
0,168 \times 2 = 0,336 \quad (\text{целая часть } 0)
$$
$$
0,336 \times 2 = 0,672 \quad (\text{целая часть } 0)
$$
$$
0,672 \times 2 = 1,344 \quad (\text{целая часть } 1)
$$
$$
0,344 \times 2 = 0,688 \quad (\text{целая часть } 0)
$$
$$
0,688 \times 2 = 1,376 \quad (\text{целая часть } 1)
$$
$$
0,376 \times 2 = 0,752 \quad (\text{целая часть } 0)
$$
$$
0,752 \times 2 = 1,504 \quad (\text{целая часть } 1)
$$

Мы можем продолжить этот процесс, но для удобства останавливаемся на $10$-м шаге. Записываем целую часть сверху вниз.
Таким образом, дробная часть $0,021$ в двоичной системе примерно равна $000001_2$ (при точности 10 знаков после запятой).
Почему примерно? Мы взяли первые шесть цифр дробной части, посчитав что такой точности достаточно.

#### 1.3. Объединение целой и дробной части
Теперь объединяем целую часть и дробную:

$$
42,021_{10} = 101010,000001_2
$$

### Шаг 2: Нормализация числа {id="2_3"}

Нормализовать число — это привести его к виду, где перед запятой будет стоять единица. Для этого сдвигаем запятую на 
несколько позиций влево.

$$
101010,000001_2 \rightarrow 1,01010000001_2 \times 2^5
$$

Мы сдвинули запятую на 5 позиций влево, поэтому степень двойки (порядок) будет равна 5.

### Шаг 3: Определение компонентов IEEE 754

IEEE 754 использует три компонента для представления вещественного числа:
- **Знак** (1 бит)
- **Порядок** (8 бит)
- **Мантисса** (23 бита)

#### 3.1. Знак
Поскольку число $42,021$ положительное, то **бит знака** будет равен $0$.

#### 3.2. Порядок
Порядок равен 5 (так как мы сдвинули запятую на 5 позиций влево). В формате IEEE 754 порядок кодируется с использованием 
смещения (bias). Для формата с одинарной точностью (32 бита) смещение равно $127$.

Значение порядка $E$ с учётом смещения:

$$
E = 5 + 127 = 132
$$

Теперь преобразуем $132$ в двоичную систему:

$$
132_{10} = 10000100_2
$$

Так что порядок в двоичном представлении будет $10000100_2$.

#### 3.3. Мантисса {id="3-3_1"}
Мантисса — это значимая часть числа без ведущей единицы (так как она всегда равна $1$ в нормализованном представлении). 
Мы оставляем только цифры после запятой:

$$
1,01010000001_2 \quad \text{(мантисса без ведущей единицы)}
$$

Остальные биты дополняем нулями до 23 бит:

$$
01010000010000000000000_2
$$

### Шаг 4: Запись числа в формате IEEE 754

Теперь мы можем собрать все части вместе:

- **Знак**: $0$
- **Порядок**: $10000100_2$
- **Мантисса**: $01010000010000000000000_2$

Записываем всё это в виде:

$$
0 \, \text{(знак)} \, | \, 10000100 \, \text{(порядок)} \, | \, 01010000010000000000000 \, \text{(мантисса)}
$$

Итак, окончательное представление числа $42,021$ в формате IEEE 754 (32-битное) будет:

$$
0 \, 10000100 \, 01010000010000000000000
$$

Это было совсем не много математики необходимой для понимания двоичной системы счисления и как числа хранятся в памяти в
двоичном виде, а так же сколько бит памяти для этого требуется.

А теперь возвращаемся к теме переменных.

## Основные правила именования переменных в C#
1. **Определение переменной:**
   - Перед использованием переменную необходимо определить.
   - Синтаксис определения переменной:
     ```c#
     тип имя_переменной;
     ```
2. **Требования к имени переменной:**
   - Имя может содержать **буквы, цифры и символ подчеркивания** (`_`).
   - **Первый символ** имени должен быть **буквой или символом подчеркивания**.
   - **Запрещено** использовать пробелы, знаки пунктуации или специальные символы.
   - Имя **не может быть ключевым словом** языка C# (например, `int`, `class` и т.д.).
   - **Чувствительность к регистру**: `age` и `Age` считаются разными именами.

3. **Стиль именования:**
   - Используйте **camelCase** для локальных переменных и полей с модификатором `private`.
   - Используйте **PascalCase** для открытых (`public`) полей, свойств, методов и имен типов.

4. **Семантическая ясность:**
   - Имя должно быть **осмысленным** и отражать суть переменной. Например, вместо `x` лучше использовать `age`, `totalAmount`, и т.д.
   - Избегайте слишком длинных или слишком коротких имен, если это не оправдано.

5. **Особые правила:**
   - Для полей класса рекомендуется использовать префикс `_` (например, `_totalAmount`) в закрытых (`private`) переменных.
   - Константы (`const`) и статические переменные (`static readonly`) именуются **заглавными буквами** с подчеркиванием (`UPPER_CASE_WITH_UNDERSCORES`).

### Таблица стилей именования и использования
| **Стиль**             | **Примеры**                  | **Использование**                                                                 |
|------------------------|------------------------------|-----------------------------------------------------------------------------------|
| **Верблюжий регистр (camelCase)** | `totalAmount`, `orderDetail` | Локальные переменные, закрытые (`private`) поля.                                 |
| **Прописной стиль (PascalCase)** | `Name`, `TotalAmount`, `Run` | Имена типов, открытых (`public`) полей, свойств, методов, классов.               |
| **Заглавные буквы (UPPER_CASE)** | `MAX_VALUE`, `DEFAULT_PORT`  | Константы и статические поля (`const`, `static readonly`).                        |

### Примеры использования:
- Локальная переменная:
  ```c#
  int totalAmount = 100;
  ```
- Закрытое поле класса:
  ```c#
  private int _totalAmount;
  ```
- Открытое свойство:
  ```c#
  public int TotalAmount { get; set; }
  ```
- Константа:
  ```c#
  private const int MAX_USERS = 1000;
  ```

Перед типами переменных, в примерах выше стоят инструкции модификаторов доступа. Всё это было кратко описано в главе 
["Элементы языка C#"](GrammarAndTerminologyCSharp.md).

Тут мы так же немного затронули константы. Про них будет в отдельной теме.

## Объяснение переменных на примере ящиков

Переменные в C# можно сравнить с **ящиками разных размеров и форм**, которые предназначены для хранения определённых данных.

1. **Размер ящика определяет вместимость**:
    - Тип `byte` — это маленький ящик, в который можно поместить числа от 0 до 255. Пример: он подходит для хранения небольших значений, таких как количество страниц книги.
    - Тип `int` — это больший ящик для чисел от -2,147,483,648 до 2,147,483,647. Пример: он используется для хранения больших значений, например, населения города.

2. **Попытка положить больше, чем ящик может вместить**:
    - Если вы попытаетесь положить число типа `int` в переменную типа `byte`, программа выдаст ошибку. Но если использовать явное преобразование `(byte)`, данные могут потеряться. Например, число 300, преобразованное в `byte`, станет 44 (остаток от деления 300 на 256).

3. **Ящики разной формы**:
    - Переменная типа `int` хранит только числа. Попытка присвоить текст (например, `"Привет"`) вызовет ошибку, потому что текст — это данные другой формы, для которых используется тип `string`.

4. **`var`: автоматический выбор ящика**:
    - Если вы используете ключевое слово `var`, программа сама выбирает размер и форму ящика в зависимости от значения, которое вы кладёте в переменную. **Важно**:
        - Переменная должна быть сразу инициализирована значением.
        - Тип переменной фиксируется при создании и не может быть изменён в дальнейшем.
      ```c#
      var x = 42; // Программа определяет, что x — это int
      x = 100;    // Это разрешено, так как новое значение тоже int
      // x = "Ошибка"; // Это вызовет ошибку, так как x — это int
      ```

5. **Изменение содержимого переменной**:
    - На протяжении программы переменной можно присваивать разные значения (но одного типа). Например, переменная `int` может содержать сначала число 42, затем 100.

6. **На каждый ящик наклеена этикетка с именем ящика. Это и есть имя переменной**.

Попрактикуемся, падаван.

Создай консольное приложение `ex0038_box_var` в папке `episode02` и добавь его в файл решения `episode02.sln`. 
Это можно сделать как в командной строке, так и в любой IDE.

Приведи Program.cs к следующему виду:

```c#
class Program
{
    static void Main()
    {
        // Маленький ящик для чисел (byte)
        byte smallBox = 100; 
        Console.WriteLine($"Маленький ящик (byte): {smallBox}");

        // Большой ящик для чисел (int)
        int bigBox = 500; 
        Console.WriteLine($"Большой ящик (int): {bigBox}");

        // Преобразование int в byte с потерей данных
        smallBox = (byte)bigBox; 
        Console.WriteLine($"Маленький ящик после преобразования (byte): {smallBox}");

        // Ящик для текста (string)
        string textBox = "Привет, мир!"; 
        Console.WriteLine($"Ящик для текста (string): {textBox}");

        // Автоматический выбор ящика с var
        var autoBox = 42; 
        Console.WriteLine($"Автоматический ящик (var, int): {autoBox}");

        // Изменение значения autoBox (тип остаётся int)
        autoBox = 1000; 
        Console.WriteLine($"Автоматический ящик с новым значением: {autoBox}");

        // Попытка присвоить текст вызовет ошибку
        // autoBox = "Ошибка"; // Нельзя, так как autoBox — это int
    }
}
```

### Результат работы программы

```
Маленький ящик (byte): 100
Большой ящик (int): 500
Маленький ящик после преобразования (byte): 244
Ящик для текста (string): Привет, мир!
Автоматический ящик (var, int): 42
Автоматический ящик с новым значением: 1000  
```

### Пояснение ключевых моментов:

1. **Инициализация `var`:**
    - Переменная `var` должна быть инициализирована сразу. Например:
      ```c#
      var myVar; // Ошибка: myVar не инициализирован
      myVar = 42; // Это недопустимо
      ```
    - Верный способ:
      ```c#
      var myVar = 42; // Программа определяет, что myVar — это int
      ```

2. **Приведение типов:**
    - Явное преобразование `(byte)bigBox` необходимо, если нужно поместить данные из большого ящика (`int`) в маленький (`byte`). Потеря данных происходит, если число слишком велико.

3. **Фиксированный тип переменной:**
    - После инициализации переменная сохраняет свой тип. Например, переменная `autoBox`, инициализированная как `int`, не может позже стать `string`.

## Ключевое слово var {id="var_1"}

`var` — это ключевое слово в C#, которое позволяет объявлять переменную без явного указания её типа.
Вместо этого **компилятор определяет тип данных по значению, введенному вами после операции присваивания (`=`)**.
Это удобно, когда тип переменной очевиден из контекста, и вам не нужно писать его явно.

### Зачем нужен `var`? {id="var_2"}

1. **Упрощает код**: Использование `var` уменьшает длину строки кода, особенно для сложных типов.
2. **Улучшает читаемость**: В некоторых случаях проще понять, что делает код, если используется `var`.
3. **Обеспечивает гибкость**: Тип данных автоматически определяется, что делает код более универсальным.

### Ограничения `var` {id="var_3"}

1. **Только локальные переменные**:
   Вы **не можете использовать `var` для переменных на уровне класса или поля**. Причина в том, что компилятор должен точно знать тип переменной во время компиляции, а на уровне класса это невозможно определить без явного типа.

   Пример (ошибка):
   ```c#
   public class MyClass
   {
       var field; // Ошибка: var нельзя использовать для полей класса
   }
   ```

2. **Обязательное присваивание при объявлении**:
   ```c#
   var x; // Ошибка: компилятор не может определить тип данных
   ```

### Примеры использования `var`

#### Для типов значений:
```c#
var age = 25; // Компилятор определяет тип как int
var price = 19.99; // Компилятор определяет тип как double
var isAlive = true; // Компилятор определяет тип как bool
```

#### Для ссылочных типов:
```c#
var name = "Alice"; // Компилятор определяет тип как string
var list = new List<int> { 1, 2, 3 }; // Компилятор определяет тип как List<int>
var person = new Person { Name = "Bob", Age = 30 }; // Компилятор определяет тип как Person
```

#### Для анонимных типов:
```c#
var user = new { Name = "Charlie", Age = 28 }; // Тип определён как анонимный объект
```

И снова практика!

Создай консольное приложение `ex0047_var_var` с помощью шаблона `tinyconsole` в папке `episode02` и добавь его в файл решения `episode02.sln`.
Это можно сделать как в командной строке, так и в любой IDE.

Приведи Program.cs к следующему виду:

```c#
using System.Collections.Generic;

public class VarExample
{
    public static void Main()
    {
        // Пример с типами значений
        var number = 42; // Компилятор определяет тип как int
        var pi = 3.14; // Компилятор определяет тип как double
        var isHappy = true; // Компилятор определяет тип как bool

        // Пример с ссылочными типами
        var message = "Hello, World!"; // Компилятор определяет тип как string
        var numbers = new List<int> { 1, 2, 3 }; // Компилятор определяет тип как List<int>
        
        // Пример с анонимным типом
        var student = new { Name = "Alice", Grade = "A" }; // Компилятор определяет тип как анонимный объект

        // Вывод данных
        WriteLine($"Number: {number}, Type: {number.GetType()}");
        WriteLine($"Pi: {pi}, Type: {pi.GetType()}");
        WriteLine($"IsHappy: {isHappy}, Type: {isHappy.GetType()}");
        WriteLine($"Message: {message}, Type: {message.GetType()}");
        WriteLine($"Numbers: {string.Join(", ", numbers)}, Type: {numbers.GetType()}");
        WriteLine($"Student: {student.Name}, {student.Grade}, Type: {student.GetType()}");
    }
}
```

Вывод программы:

```
Number: 42, Type: System.Int32
Pi: 3,14, Type: System.Double
IsHappy: True, Type: System.Boolean
Message: Hello, World!, Type: System.String
Numbers: 1, 2, 3, Type: System.Collections.Generic.List`1[System.Int32]
Student: Alice, A, Type: <>f__AnonymousType0`2[System.String,System.String]
```

### Пояснение программы

1. **Типы значений**:
    - `var number = 42;` — переменная `number` автоматически получает тип `int`.
    - `var pi = 3.14;` — переменная `pi` автоматически получает тип `double`.

2. **Ссылочные типы**:
    - `var message = "Hello, World!";` — переменная `message` получает тип `string`.
    - `var numbers = new List<int> { 1, 2, 3 };` — тип переменной `numbers` — `List<int>`.

3. **Анонимный тип**:
    - `var student = new { Name = "Alice", Grade = "A" };` — тип переменной определяется как анонимный объект с полями `Name` и `Grade`.

4. **Вывод типов**:
    - Используется метод `GetType()`, чтобы показать, какие типы компилятор назначил переменным.

### Итог
Ключевое слово `var` — это инструмент, который помогает сократить код и повысить его читаемость.
Однако важно помнить, что оно не меняет саму строгость типов в C#: компилятор всегда точно знает тип переменной.
Используйте `var` с учётом контекста, чтобы ваш код был одновременно лаконичным и понятным.

## Объяснение операции присваивания

Операция присваивания (`=`) в программировании может показаться странной, если рассматривать её с точки зрения математики. 
Например, выражение:

```c#
i = i + 42;
```

С математической точки зрения кажется нелогичным, ведь $ i \neq i + 42 $. Но в программировании это работает иначе. 
Операция присваивания означает: **взять значение справа, выполнить расчёты (если есть), и поместить результат в 
переменную слева**.

- **Правая часть** выражения вычисляется сначала. Например, если `i = 10`, то `i + 42` становится `52`.
- Затем результат (`52`) **перезаписывает** старое значение переменной `i`. Теперь `i` равен `52`.

Пример:  
Представьте ящик с надписью «i». Если в нём лежит число `10`, то выражение `i = i + 42` говорит: 
возьми содержимое ящика, прибавь `42`, и положи обратно результат (`52`).

## Вывод значений переменных в консоль

Чтобы показать значение переменной в консоли, вы можете использовать несколько способов:

### Старый способ: конкатенация строк
Этот способ объединяет строки и значения переменных с помощью символа `+`. Например:
```c#
int i = 10;
Console.WriteLine("i = " + i);
```
Выводит:
```
i = 10
```

### Новый способ: интерполяция строк
Более современный и удобный способ в C# — использовать **интерполяцию строк**. Перед строкой ставится знак `$`, а переменные вставляются в строку внутри фигурных скобок `{}`:
```c#
int i = 10;
Console.WriteLine($"i = {i}");
```
Вывод будет таким же:
```
i = 10
```

Практика!

Создай консольное приложение `ex0039_set_var` в папке `episode02` и добавь его в файл решения `episode02.sln`.
Это можно сделать как в командной строке, так и в любой IDE.

Приведи Program.cs к следующему виду:

```c#
class Program
{
    static void Main()
    {
        // Присваивание
        int i = 10; // Создаём коробку (переменную i) и кладём туда число 10
        Console.WriteLine($"Начальное значение i: {i}");

        i = i + 42; // Перезаписываем i, добавив 42
        Console.WriteLine($"Новое значение i после i = i + 42: {i}");

        // Демонстрация вывода разными способами
        Console.WriteLine("Старый способ: i = " + i);  // Конкатенация
        Console.WriteLine($"Новый способ: i = {i}");  // Интерполяция строк
    }
}
```
### Результат работы программы

```
Начальное значение i: 10
Новое значение i после i = i + 42: 52
Старый способ: i = 52
Новый способ: i = 52
```

Про работу со строками мы поговорим чуть позже и более подробно. А пока достаточно этого для выполнения упражнений.

> Почему вдруг такие номера в названиях программ? А потому что 😊 я сперва написал раздел по переменным типов значений,
> а потом подумал, что надо бы более доходчиво объяснить понятие переменных, для тех кто только столкнулся с этой темой.
{style="note"}

## Что дальше?

Далее вам надо будет изучить два достаточно больших раздела:
- [Переменные типов значений](value-vasr-in-csharp.md)
- [Переменные ссылочных типов](ref-type-vars.md)

Что это за типы, а тем более кто их сослал в ссылку вы узнаете по ходу повествования 😊

Сразу могу сказать, что чтиво будет достаточно нудное и мозгопарительное. Относитесь к этому как к изучению слов в обычном
иностранном языке. Знания самих слов не достаточно, чтобы говорить на языке, но знать слова необходимо. Это так сказать
минимальный минимум 😊

Но по крайней мере вы уже будете хоть что-то понимать в коде. Не всё, но достаточно много.

В этих разделах достаточно много упражнений. Рекомендую все их набирать ручками, а не копировать код с сайта. Так вы больше
будете понимать.

Кроме того, очень рекомендую выполнять схемы обучения на сайте Microsoft. Там тоже есть теория и практика.

Зарегистрируйтесь на сайте обучения, чтобы сохранялись ваши результаты.

Начать можно с этой самой первой схемы обучения: [Начало работы с C#, часть 1](https://learn.microsoft.com/ru-ru/training/paths/get-started-c-sharp-part-1/).

Предварительно рекомендую, всё же, изучить раздел [Переменные типов значений](value-vasr-in-csharp.md). Ну или обращаться
к нему за справкой. Хотя, конечно же, всё можно изучать параллельно. Одно будет дополнять другое. Да и практики много не бывает.

Запускать примеры программ схем обучения можно прямо на сайте Microsoft. Это удобно для обучения, но в реальной практике
программирования вы так сделать не сможете. Вам надо будет создавать свои проекты. Поэтому очень рекомендую после решения
задач на сайте Microsoft, писать те же самые программы у себя на компьютере.

Например, вот так выглядит решение задачи на сайте Microsoft:

![Начало работы с C#](MS01.png){ border-effect="line"  thumbnail="true" width="700" }

Как видите на сайте вам не надо создавать проект, править файлы и запускать его из командной строки или IDE. Поэтому
я очень рекомендую все упражнения которые вы делаете на сайте, так же делать у себя и на компе, создавая для каждого
отдельный проект. Ну или если упражнения простые, то делать это в одном проекте.

В общем чем больше у вас будет практики, тем лучше для вас.

## Немного магии начального уровня {id=magic}

Эту часть вам следует прочитать после того как вы изучите переменные типов значений и ссылочных типов. А возможно даже и 
классы. Я решил разместить этот материал тут, так как в разделе ["Ключевое слово var"](#var_1) был затронут интересный
вопрос, который у вас должен будет возникнуть в будущем после изучения классов. Этот вопрос, относительно программы
`ex0047_var_var` должен звучать примерно так:

*"Интересно ведь number это переменная типа значения, то есть не класс и не ссылочный тип. 
От куда у неё берется метод GetType(), ведь методы это часть класса?"*

Если вы только начали изучать C#, то эта часть силы знания скрыта от вас. Но по идее потом, если у вас пытливый ум,
такой вопрос должен возникнуть.

Поэтому пока можете просто прочитать для информации, но после изучения указанных выше тем, лучше вернуться с обретенной
силой знания и прочитать снова.

### Что такое `GetType()`?

Метод `GetType()` возвращает тип объекта. Например, если переменная — это число, `GetType()` скажет, что это `int`. Но 
если методы — это часть классов, как же тогда переменная типа значения, например `int`, имеет этот метод?

### Почему `int` имеет метод `GetType()`?

1. **Типы значений в C# — это тоже структуры**:
   В C#, типы значений (такие, как `int`, `double`, `bool`) — это не совсем "просто числа". На самом деле они — **структуры** 
2. (структуры — это такие же объекты, как классы, только работают более "легковесно").

   Например:
    - `int` — это структура `System.Int32`.
    - `double` — это структура `System.Double`.
    - `bool` — это структура `System.Boolean`.

   Эти структуры уже имеют встроенные методы, такие как `GetType()`.

2. **Все структуры и классы наследуют `Object`**:
   В C# все типы, включая структуры и классы, неявно наследуют базовый класс `System.Object`. Это значит, что любой объект, будь то структура или класс, имеет доступ к методам из `System.Object`.

   Одним из таких методов является `GetType()`.

### Как это работает на практике?

Когда вы создаёте переменную типа значения, например:

```c#
int number = 42;
```

На самом деле, вы создаёте объект структуры `System.Int32`, которая ведёт себя как тип значения. Этот объект уже содержит метод `GetType()`, унаследованный от `System.Object`.

Чтобы лучше понять давайте представим, что типы значений — это тоже как бы "младшие братья классов". Они не такие сложные, как классы, но унаследовали некоторые "навыки" от главного "родителя" — `Object`. Одним из таких навыков является метод `GetType()`.

Когда вы пишете:

```c#
int number = 42;
Console.WriteLine(number.GetType());
```

Это похоже на то, как если бы младший брат (`int`) сказал: "Я умею говорить о своём типе, потому что этому научил меня 
мой родитель `Object`."

Попрактикуемся, чтобы понять идею.

Создай консольное приложение `ex0048_magic` с помощью шаблона `tinyconsole` в папке `episode02` и добавь его в 
файл решения `episode02.sln`. Это можно сделать как в командной строке, так и в любой IDE.

Приведи Program.cs к следующему виду:

```c#
public class ValueTypeExample
{
    public static void Main()
    {
        // Тип значения
        int number = 42;
        double pi = 3.14;
        bool isHappy = true;

        // Вызов метода GetType()
        WriteLine($"number: {number}, Type: {number.GetType()}"); // System.Int32
        WriteLine($"pi: {pi}, Type: {pi.GetType()}"); // System.Double
        WriteLine($"isHappy: {isHappy}, Type: {isHappy.GetType()}"); // System.Boolean
    }
}
```

Вывод программы:

```
number: 42, Type: System.Int32
pi: 3,14, Type: System.Double      
isHappy: True, Type: System.Boolean
```

### Что происходит?

1. `number.GetType()` вызывает метод `GetType()`, который возвращает тип `System.Int32`.
2. Компилятор знает, что `int` — это `System.Int32`, и вызов `GetType()` работает, потому что `System.Int32` наследует `Object`.

### Итог

- Типы значений, такие как `int`, на самом деле являются структурами, а структуры могут содержать методы.
- Все типы, даже типы значений, наследуют `Object`, который предоставляет метод `GetType()`.
- Поэтому, даже если `int` выглядит как "простое число", оно обладает методами благодаря тому, что является объектом `System.Int32`.

> **Представьте, что каждый объект в C# — это как человек с удостоверением личности. У каждого есть метод `GetType()`, 
> который говорит, кто он такой. Даже простое число — не исключение.**

