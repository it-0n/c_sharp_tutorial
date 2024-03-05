# Установка Visual Studio Code в Windows
Установка Visual Studio Code в любой ОС очень простая. Что уж говорить про винду, поэтому я пока напишу об этом вкратце.
Как будет время опишу установку более подробно со скриншотами.

## Краткое описание установки VSCode в Windows
Идем на [сайт Visual Studio Code](https://code.visualstudio.com/), качаем установщик и устанавливаем :) Что уж проще? 

![Загрузка VS Code](VSCode01.png){border-effect="line" thumbnail="true" width="621"}

После установки VSCode (так сокращенно называют Visual Studio Code), необходимо установить плагины для разработки приложений
на C#. Хотя по существу надо установить один плагин [C# Dev Kit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit), а он уже подтянет сам несколько других, которые ему необходимы
для работы.

Для установки плагина запускаете VSCode, затем кликаете по иконке управления плагинами, в поиске вводите **C# Dev Kit**.
И затем жмете кнопку установить. После установки надо будет перезапустить VSCode.

![Установка плагина C# Dev Kit для VSCode](VSCode02.png){border-effect="line" thumbnail="true" width="621"}

>У меня плагины уже установлены, поэтому рядом с ними нет кнопочки установить.
{style="note"}

Так же установите плагин [WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl).

![Установка плагина WSL для VSCode](VSCode03.png){border-effect="line" thumbnail="true" width="621"}

Этого уже достаточно, чтобы начать разрабатывать программы на C# в VSCode.