# Структура проекта C#

Мы уже немного говорили на эту тему [тут](Install-Visual-Studio-Code-in-Windows.md#csharp_files_and_folders). Сейчас мы 
немного больше углубимся в эту тему. И начнем сразу с практики. Создайте проект `ex0012_default_namespaces` в JetBrains Rider.
Проект должен быть в решении episode02.

![Создание проекта в JetBrains Rider](NameSpaces01.png){ border-effect="line"  thumbnail="true" width="700" }

В результате у вас должно получиться что-то вроде такого:

![Проекты в JetBrains Rider](NameSpaces02.png){ border-effect="line"  thumbnail="true" width="700" }

Теперь мы посмотрим какие пространства имен (namespaces) были импортированы нашей программой. Кстати это мы уже делали
[тут](how-to-crate-csharp-windows-command-line.md#RiderDefaultNamespace). Рекомендую освежить это в памяти.

На скриншоте выше вы видите фигурные скобки в области нумерации строк у первой строки. Наведите на нее мышь.

![Проекты в JetBrains Rider](NameSpaces03.png){ border-effect="line"  thumbnail="true" width="700" }

Вы должны увидеть подсказку **Global 'using' directives**. Как раз о глобальном явном и неявном импортах мы сейчас и будем
говорить.

Далее кликните по этим фигурным скобкам мышкой. И вы должны увидеть следующее:

![Проекты в JetBrains Rider](NameSpaces04.png){ border-effect="line"  thumbnail="true" width="700" }

Ну можно сказать преступление раскрыто! Мы вышли на след файла где неявно импортируются пространства имен. Этот файл
создается в подкаталоге obj во время создания проекта. Имя файла всегда стандартное. Сперва идет имя проекта, 
потом точка, а за ним **GlobalUsings.g.cs**.