# Обновление .NET SDK в Windows
Обновления .NET SDK не происходит автоматически, как других компонентов Windows. Чтобы обновить .NET SDK, необходимо
[скачать](https://dotnet.microsoft.com/en-us/download/dotnet) новую версию и установить ее.

На момент написания этой статьи уже вышло обновление для .NET SDK 8.0.

![Обновление .NET SDK 8 в Windows](upgradeDonNetWindows02.png){border-effect="line" thumbnail="true" width="700"}

В командной строке Windows дайте команду `dotnet --info`

![Обновление .NET SDK 8 в Windows](upgradeDonNetWindows01.png){border-effect="line" thumbnail="true" width="700"}

Скачиваем новую версию .NET SDK для своей платформы, в большинстве случаев то это x64. И затем
устанавливаем [как обычно](Install-NET-SDK-8-in-Windows.md).

![Обновление .NET SDK 8 в Windows](upgradeDonNetWindows03.png){border-effect="line" thumbnail="true" width="700"}

Снова в командной строке Windows дайте команду `dotnet --info`

![Обновление .NET SDK 8 в Windows](upgradeDonNetWindows04.png){border-effect="line" thumbnail="true" width="700"}

Обратите внимание, что теперь установлены две версии .NET SDK 8.0. То есть новая версия встала рядом со старой, но по
умолчанию будет использоваться новая версия.

В панели управления в оснастке удаления программ можно увидеть то же самое.

![Обновление .NET SDK 8 в Windows](upgradeDonNetWindows05.png){border-effect="line" thumbnail="true" width="700"}

Но для версии .NET SDK 8.0.202 видно, что эта версия была установлена вместе с Visual Studio. 

>Ни когда не удаляйте версию .NET SDK установленную вместе с Visual Studio, если только не хотите огрести проблем.
{style = warning}