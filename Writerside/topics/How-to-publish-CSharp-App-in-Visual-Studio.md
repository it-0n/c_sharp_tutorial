# Публикация приложения C# в Visual Studio
Публиковать приложения в Visual Studio, конечно гораздо проще чем в командной строке.

## Публикация автономного приложения для Windows x64 в Visual Studio

Давайте откроем проект
ex0005_hello_os.

>У меня интерфейс Visual Studio на английском, выбрана темная тема, и кастомизировано положение **Обозревателя решений**
(Solution Explorer). У меня он находится с левой стороны, тогда как по умолчанию после установки он располагается с левой.
Не пугайтесь английскому языку, а так же немного другому виду Visual Studio. Вникайте в суть. Далее по курсу, я буду
чаще использовать версию Visual Studio с английским интерфейсом, если вы установили с русским, то вам надо находить разные
пункты меню и окон на русском самостоятельно. Считайте это заданием, или переключите студию на английский интерфейс.
{style = note}

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

Далее выставляем всё как на скриншоте. То есть мы создаем автономный исполняемый файл. По существу мы делаем тоже самое,
когда публиковали автономное приложение для Linux средствами CLI, только в этот раз делаем автономное приложение для
Windows x64. Жмём **Save**

![Публикация приложения C# в Visual Studio](PublishByVisualStudio08.png){ border-effect="line"  thumbnail="true" width="700"}

Далее жмём **Pubish**

![Публикация приложения C# в Visual Studio](PublishByVisualStudio09.png){ border-effect="line"  thumbnail="true" width="700"}

Visual Studio сформирует один исполняемый файл. Чтобы увидеть его нажмите **Open folder**.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio10.png){ border-effect="line"  thumbnail="true" width="700"}

Вот собственно и наш файл. Теперь вы можете запускать его на любом компьютере с ОС Windows x64, даже если там не установлен .NET Runtime.

![Публикация приложения C# в Visual Studio](PublishByVisualStudio11.png){ border-effect="line"  thumbnail="true" width="700"}

