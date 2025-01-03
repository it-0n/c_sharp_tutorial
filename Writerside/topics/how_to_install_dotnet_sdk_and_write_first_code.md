# Установка .NET SDK и первая программа на C#

Эти статьи можно не читать если вы знаете ответы на эти вопросы:

- [Как установить .NET SDK в Windows](Install-NET-SDK-8-in-Windows.md)
- [Как установить .NET SDK в WSL (Windows Subsystem for Linux)](Install-NET-SDK-8-in-WSL.md)
- [Как установить .NET SDK в Linux](How-to-install-NET-SDK-in-Linux.md)
- [Как установить .NET SDK в macOS](Install-NET-SDK-in-macOS.md)
- [Как в командной строке создать проект C#](how-to-crate-csharp-windows-command-line.md)
- Как запустить приложение (программу) из созданного проекта в командной строке
- [Как создать решение и проект C# в Visual Studio](Install-Visual-Studio-2022.md#How-to-crate-solution-in-VisualStudio)
- [Как создать решение и проект C# в JetBrains Rider](Install-JetBrains-Rider-in-Windows.md#how-to-create-solution-in-rider)
- [Как сделать сборку проекта, чтобы его можно было запустить на других компьютерах](How-to-Publish-CSharp-Program-App.md)

Конечно же вы можете использовать только те части уроков, которые относятся к вашей ОС. Но я бы рекомендовал установить
виртуальную машину с теми ОС которых у вас нет и выполнять упражнения на всех трех ОС. Если вы не знаете что такое виртуальная
машина, то забейте, но лучше конечно погуглите, посмотрите видосики и установите необходимые виртуалки.

И так, падаван, начнем с выбора оружия, вернее рабочего окружения 😊

В первом бою нам понадобиться:
- .NET SDK
- Текстовый редактор

Текстовый редактор подойдет любой, лиж бы мог сохранять текст в кодировке UTF-8. Для Windows подойдет даже блокнот.
Для Linux или macOS подойдет любой текстовый редактор входящий в стандартную поставку ОС.

Не пугайтесь, все время в блокноте писать не будем 😊. Я не садист 😊. Просто для написания простого когда первых упражнений
не нужна тяжелая IDE, типа Visual Studio для Windows или macOS, или даже продвинутый редактор Visual Studio Code.

Написать 5 - 10 строк кода можно и в текстовом редакторе. А в вашем случае, вообще скопировать код из этого учебника,
вставить в редактор и сохранить. Хотя конечно лучше чтобы вы его набрали сами.

Я всегда за практику. Поэтому предлагаю вам не копировать код с этого учебника, а набирать его самим и делать это вдумчиво.
Но это так совет, конечно вы можете делать как вам удобно.

Просто на мой взгляд, когда вы сами набираете код, то вы лучше начинаете понимать то что делаете, так как прилагаете к этому усилие.
Тем более если вы только начинаете изучать программирование.

Далее выбираете статью для вашей ОС и текущего SDK.

На текущий момент актуальной версией .NET SDK является 8 версия. Но по ходу выхода новых версий будут добавляться 
соответствующие статьи (старые убираться не будут)