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


