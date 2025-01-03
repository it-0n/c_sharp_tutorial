# Установка .NET 8.0 SDK в Linux
[Установка .NET SDK в разных дистрибутивах Linux](https://learn.microsoft.com/en-us/dotnet/core/install/linux) тянет на 
отдельную большую статью, а не на коротенький урок. Можете пройти по линку и посмотреть. В инструкциях на сайте Микрософт
на данную тему легко запутаться даже не самому начинающему человеку, поскольку есть несколько вариантов установки.

Я постепенно буду наполнять данный раздел инструкциями для всех дистрибутивов Linux, на которых я устанавливал 
.NET SDK, но пока начну с основных дистрибутивов и с самых простых способов.

## Установка .NET SDK в Ubuntu
В следующей таблице приведен список поддерживаемых Микрософт выпусков .NET и версий Ubuntu, в которых они поддерживаются. 
Хоть данная таблица взята с сайта Микрософт, но даже на март 2024 года она не совсем актуальна. 

Более актуальную информацию смотрите [тут](https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu#supported-distributions).
Хотя, как вы видите, даже на сайте Микрософт актуализация информации может запаздывать.

![Таблица поддерживаемых в Ubuntu версий .NET](UbuntuNETInstall01.png)

В третьей колонке таблицы (Ubuntu feed) мы видим что для Ubuntu 22.04 доступны только версии .NET 7.0 и 6.0, но на самом 
деле на февраль 2024 доступна так же и версия 8.0. Ubuntu feed означает родные репозитории Ubuntu.

Так же из данной таблицы видно, что наиболее широкий спектр версий .NET SDK возможен для Ubuntu 20.04, которая будет
поддерживаться до апреля 2030 года. Кстати время поддержки разных версий Ubuntu можно посмотреть [здесь](https://wiki.ubuntu.com/Releases).
Это важно знать, так как когда версия Ubuntu перестает поддерживаться, .NET больше не поддерживается этой версией.

Я уже говорил что установка .NET SDK в Linux, и [в частности, в Ubuntu возможна несколькими способами](https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu#decide-how-to-install-net).
Все эти способы имеют свои плюсы и минусы показанные в таблице ниже:

![Таблица вариантов установки .NET SDK в Ubuntu](UbuntuNETInstall04.png)

Если эти таблички вам ни о чём не говорят и вы не понимаете к чему я это всё написал, то просто забейте. Поймете чуть позже. 😊

Далее будут описаны разные способы установки .NET SDK в Ubuntu, начиная с самого простого. Описание способов установки 
будет добавляться очень постепенно 😊

### Установка .NET SDK 8.0 в Ubuntu 22.04 из репозитория Ubuntu
Установка .NET SDK 8.0 в Ubuntu 22.04 ни чем не отличается от того как это было сделано в [статье по установке .NET SDK
для WSL Ubuntu](Install-NET-SDK-8-in-WSL.md#Install_DotNetSKD_WSL_Ubuntu). Это делается командой:

`sudo apt install dotnet-sdk-8.0 -y`

![Установка .NET SDK 8.0 в Ubuntu 22.04](UbuntuNETInstall02.png){border-effect="line" thumbnail="true" width="621"}

На скриншоте выше я сперва дал команду вывода версии дистрибутива Ubuntu, чтобы показать, что установка делается именно
в Ubuntu 22.04, а затем уже дал команду установки .NET SDK 8.0.

Проверим что .NET SDK 8.0 действительно установился командой: 

`dotnet --info`

А так же проверим что .NET SDK 8.0 был установлен из репозитория Ubuntu командой:

`apt policy dotnet-sdk-8.0`

![Проверка установки .NET SDK 8.0 в Ubuntu 22.04](UbuntuNETInstall03.png){border-effect="line" thumbnail="true" width="621"}
