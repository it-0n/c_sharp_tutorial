# Публикация приложения C# в JetBrains Rider
Публикация приложения в JetBrains Rider, так же проста, как и в Visual Studio. Но Visual Studio не умеет работать с WSL,
что кстати очень странно, так как и то и другое разрабатывает Микрософт. Поэтому, для разнообразия и опыта, мы сделаем
публикации в Rider в среде WSL.

## Публикация автономного приложения для Linux x64 в WSL
Запускаем Rider и выбираем WSL

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL01.png){ border-effect="line"  thumbnail="true" width="700"}

Затем жмём на плюс

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL02.png){ border-effect="line"  thumbnail="true" width="700"}

Затем выбираем проект **ex0005_hello_os**

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL03.png){ border-effect="line"  thumbnail="true" width="700"}

После запуска Rider, щёлкаем правой кнопкой мыши на названии проекта и выбираем **Publish...**

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL04.png){ border-effect="line"  thumbnail="true" width="700"}

Затем выбираем **Local folder**

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL05.png){ border-effect="line"  thumbnail="true" width="700"}

Далее все делаем как на скриншоте. После каталога publish, я добавил еще каталог Rider, чтобы было нагляднее и удобнее,
что райдер будет публиковать в этот каталог. И жмём **Run** для публикации.

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL06.png){ border-effect="line"  thumbnail="true" width="700"}

Rider какое-то время подумает и опубликует приложение. 

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL07.png){ border-effect="line"  thumbnail="true" width="700"}

Но он не будет на столько любезен как Visual Studio и не предложит сразу же открыть папку в которой находится 
опубликованное приложение. Поэтому в эту папочку придётся пройти самим. Запускаем терминал с WSL и даем последовательно
команды как на скриншоте (с поправкой на ваши пути):

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL08.png){ border-effect="line"  thumbnail="true" width="700"}

Как видите проект был опубликован, то есть создан один исполняемый файл которые в себе уже содержит .Net Runtime.
Наша программа прекрасно запускается и работает :)

## Публикация приложения C# зависимого от среды исполнения в WSL
После того как мы создали первый профиль публикации приложения, пункт меню **Publish...**, вызываемый по правому клику мыши
на имени проекта , может исчезнуть. Поэтому лучше воспользоваться методом добавления нового профиля, [описанного в документации
JetBrains](https://www.jetbrains.com/help/rider/Run_Debug_Configuration_Publish_to_Folder.html).

Для открываем наш проект в WSL, как мы уже это делали и жмем сочетание клавиш `Ctrl` `Alt` `Shift` `R`

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL09.png){ border-effect="line"  thumbnail="true" width="700"}

выбираем пункт меню **Edit Configurations...**, и вы должны увидеть что-то вроде этого

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL10.png){ border-effect="line"  thumbnail="true" width="700"}

Раскрываем узел **Publish to folder** и затем жмём на плюс (+), чтобы добавить новую конфигурацию или жмём 
**Add new run configuration...**

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL11.png){ border-effect="line"  thumbnail="true" width="700"}

И далее выбираем **Publish to folder**

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL12.png){ border-effect="line"  thumbnail="true" width="700"}

Вы должны увидеть что-то вроде этого:

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL13.png){ border-effect="line"  thumbnail="true" width="700"}

Далее заполняем поля как на скриншоте и затем жмём **Apply** и **Run**

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL14.png){ border-effect="line"  thumbnail="true" width="700"}

После этого проект будет опубликован и мы получим об этом сообщение.

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL15.png){ border-effect="line"  thumbnail="true" width="700"}

Далее запустим терминал WSL, зайдем в каталог куда был опубликован проект и запустим его.

![Публикация приложения C# в JetBrains Rider](RiderPublishWSL16.png){ border-effect="line"  thumbnail="true" width="700"}

Как видите было сгенерировано два исполняемых файла, один для Linux, другой с расширением .dll. Соответственно они запускаются
по-разному. 

Если вы помните, то когда мы публиковали приложение Framework Depended в Visual Studio, то там были созданы два файла.
Один с расширением .exe, второй с расширением .dll.

Инструмент CLI dotnet, публикует эти два файла в зависимости от платформы на которой происходит публикация. Сейчас скорее
всего вам это будет не понятно. Чтобы разобраться получше почитайте статьи на сайте Микросот, которые я привел в начале этой
главы. Но можете пока и не забивать этим голову. На данном этапе вам достаточно научиться публиковать приложения и запускать
их в различных средах.

>И кстати! Теперь вы можете использовать созданные профили публикации, чтобы публиковать приложения. Вам не нужно создавать
> заново профили публикации. Просто используйте их.
{style = note}

Удачи, падаван!