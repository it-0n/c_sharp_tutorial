# Установка .NET SDK в macOS
[.NET SDK в macOS можно установить двумя способами](https://learn.microsoft.com/ru-ru/dotnet/core/install/macos):
- автоматическая установка (используется автономный установщик)
- ручная установка 

Разработчикам рекомендуется автоматическая установка.

[Различные версии macOS поддерживают разный спектр версий .NET](https://learn.microsoft.com/ru-ru/dotnet/core/install/macos#supported-releases).

![Таблица поддерживаемых версий .NET SDK в macOS](macOSInstall01.png){border-effect="line"}

Исходя из этой таблицы выберите подходящую версию .NET для вашей версии macOS. Для большинства примеров в этом курсе 
могут подойти и .NET 6 или .NET 7, поэтому если у вас нет возможности установить .NET 8 не переживайте.

Скачивайте дистрибутив. В моём случае это был `dotnet-sdk-8.0.201-osx-x64.pkg` и устанавливайте.

![Установка .NET SDK в macOS](macOSInstall02.png){border-effect="line"}

Занимает .NET SDK конечно не мало места.

![Установка .NET SDK в macOS](macOSInstall03.png){border-effect="line"}

Далее у вас попросят ввести пароль и потом .NET SDK будет установлен.

![Установка .NET SDK в macOS](macOSInstall04.png){border-effect="line"}

По идее после окончания установки можно запустить терминал и проверить работу командой `dotnet --info`. Но иногда 
установщик не прописывает переменную окружения для .NET и не добавляет .NET в PATH. Поэтому приходится это делать вручную
или запустить установщик ещё раз.

![Проверка .NET SDK в macOS](macOSInstall05.png){border-effect="line"}


