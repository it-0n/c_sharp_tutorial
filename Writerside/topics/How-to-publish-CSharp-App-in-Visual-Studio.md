# Публикация приложения C# в Visual Studio
Публиковать приложения в Visual Studio, конечно же, гораздо проще чем в командной строке.

>У меня интерфейс Visual Studio на английском, выбрана темная тема, и кастомизированно положение **Обозревателя решений**
(Solution Explorer). В моём случае он находится с левой стороны, тогда как по умолчанию после установки он располагается с правой.
Не пугайтесь английскому языку, а так же немного другому виду Visual Studio. Вникайте в суть. Далее по курсу, я буду
чаще использовать версию Visual Studio с английским интерфейсом, если вы установили с русским, то вам надо находить разные
пункты меню и окон на русском самостоятельно. Считайте это заданием, или переключите студию на английский интерфейс.
{style = note}

## Публикация автономного приложения для Windows x64
Давайте откроем проект **ex0005_hello_os**.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio01.png){ border-effect="line"  thumbnail="true" width="700"}

Затем нажмите правой кнопкой мыши по названию проекта и выберите **Publish**

![Публикация приложения C# в Visual Studio](PublishByVisualStudio02.png){ border-effect="line"  thumbnail="true" width="700"}

Далее выбираем **Folder** и жмём **Next**.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio03.png){ border-effect="line"  thumbnail="true" width="700"}

Опять выбираем **Folder** и жмём **Next**.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio04.png){ border-effect="line"  thumbnail="true" width="700"}

Здесь всё можно оставить по умолчанию и нажать **Finish**.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio05.png){ border-effect="line"  thumbnail="true" width="700"}

Жмём **Close** без вариантов :)

![Публикация приложения C# в Visual Studio](PublishByVisualStudio06.png){ border-effect="line"  thumbnail="true" width="700"}

Таким образом мы создали профайл публикации. Теперь жмём **Show all settings**

![Публикация приложения C# в Visual Studio](PublishByVisualStudio07.png){ border-effect="line"  thumbnail="true" width="700"}

Далее выставляем всё как на скриншоте. То есть мы создаем автономный исполняемый файл. По существу мы делаем то же самое,
когда публиковали автономное приложение для Linux средствами CLI, только в этот раз делаем автономное приложение для
Windows x64. Жмём **Save**

![Публикация приложения C# в Visual Studio](PublishByVisualStudio08.png){ border-effect="line"  thumbnail="true" width="700"}

Далее жмём **Publish**

![Публикация приложения C# в Visual Studio](PublishByVisualStudio09.png){ border-effect="line"  thumbnail="true" width="700"}

Visual Studio сформирует один исполняемый файл. Чтобы увидеть его нажмите **Open folder**.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio10.png){ border-effect="line"  thumbnail="true" width="700"}

Вот собственно и наш файл. Теперь вы можете запускать его на любом компьютере с ОС Windows x64, даже если там не установлен .NET Runtime.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio11.png){ border-effect="line"  thumbnail="true" width="700"}

## Публикация приложения C# зависимого от среды исполнения
Теперь давайте добавим ещё один профайл для публикации приложения, для этого жмём **More action** и выбираем **Rename**.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio12.png){ border-effect="line"  thumbnail="true" width="700"}

Переименовываем и сохраняем.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio13.png){ border-effect="line"  thumbnail="true" width="700"}

В результате должо поучиться так:

![Публикация приложения C# в Visual Studio](PublishByVisualStudio14.png){ border-effect="line"  thumbnail="true" width="700"}

После этого жмём **New Profile** и проходим следующие, уже знакомые вам, шаги:

![Публикация приложения C# в Visual Studio](PublishByVisualStudio15.png){ border-effect="line"  thumbnail="true" width="700"}

![Публикация приложения C# в Visual Studio](PublishByVisualStudio16.png){ border-effect="line"  thumbnail="true" width="700"}

![Публикация приложения C# в Visual Studio](PublishByVisualStudio17.png){ border-effect="line"  thumbnail="true" width="700"}

![Публикация приложения C# в Visual Studio](PublishByVisualStudio18.png){ border-effect="line"  thumbnail="true" width="700"}

Результат у вас должен быть примерно такой:

![Публикация приложения C# в Visual Studio](PublishByVisualStudio19.png){ border-effect="line"  thumbnail="true" width="700"}

Далее жмём **Show all settings** и делаем всё как на скриншоте

![Публикация приложения C# в Visual Studio](PublishByVisualStudio20.png){ border-effect="line"  thumbnail="true" width="700"}

Ну и давайте сразу переименуем наш новый профайл, чтобы понимать какой тип публикации приложения он делает. Жмём 
**More actions** и выбираем **Rename**

![Публикация приложения C# в Visual Studio](PublishByVisualStudio22.png){ border-effect="line"  thumbnail="true" width="700"}

И вводим название нашего профайла.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio21.png){ border-effect="line"  thumbnail="true" width="700"}

В результате вы должны увидеть что профиль переименовался и можно жать на кнопку публикации приложения.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio23.png){ border-effect="line"  thumbnail="true" width="700"}

В результате наше приложение опубликовано и мы можем нажать **Open folder**, чтобы увидеть файлы нашего приложения.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio24.png){ border-effect="line"  thumbnail="true" width="700"}

И вот они файлы нашего приложения (обведены в красную рамку). Чтобы приложение работало их надо передавать все на компьютер
пользователя, причем у пользователя должен быть установлен .NET Runtime соответствующей версии.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio25.png){ border-effect="line"  thumbnail="true" width="700"}

Там так же видно папку win-x64, в которой находится файл предыдущей публикации.

Вообще структуру папок публикации можно было бы сделать и получше, но я оставлял все пути практически по умолчанию.

Выбрать нужный профайл для публикации можно нажав маленькую стрелочку вниз рядом с названием текущего профиля.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio26.png){ border-effect="line"  thumbnail="true" width="700"}

>Обратите внимание, что после публикаций приложения, в каталоге нашего проекта появилась новая папка Properties, 
а так же новые файлы с расширениями .user и .pubxml. В этих файлах как раз и хранятся настройки наших публикаций.
{style = note}

![Публикация приложения C# в Visual Studio](PublishByVisualStudio27.png){ border-effect="line"}