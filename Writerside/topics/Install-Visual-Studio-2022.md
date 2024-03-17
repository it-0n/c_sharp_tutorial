# Установка Visual Studio 2022 и  проверка работы
Как я уже говорил Visual Studio можно установить только в Windows. Visual Studio существует в нескольких редакциях:
- [Visual Studio Community](https://visualstudio.microsoft.com/ru/vs/community/)
- [Visual Studio Professional](https://visualstudio.microsoft.com/ru/vs/)
- [Visual Studio Enterprise](https://visualstudio.microsoft.com/ru/vs/)

Сравнение редакций Visual Studio можно посмотреть [тут](https://visualstudio.microsoft.com/ru/vs/compare/).

Скачать любую из редакций можно по ссылкам выше или по [этой](https://visualstudio.microsoft.com/ru/downloads/).

*Но есть так же и альтернативные источники загрузки ;)* И кто вам может помешать воспользоваться ими? :)

![Скачивание редакций Visual Studio](VisualSutioInstall01.png){border-effect="line" thumbnail="true" width="700"}

В этом курсе будет использована редакция с максимальными возможностями - Visual Studio Enterprise.

Скачиваем её и начинаем установку. Сам установщик весит не много. Но по ходу установки он скачивает всё необходимое из
сети. И в связи с этим есть два варианта установки:
- установка онлайн, с помощью скачанного загрузчика
- установка с предварительной загрузкой всех компонентов Visual Studio

Мы рассмотрим оба этих варианта.

## Стандартная установка (онлайн)

Скачайте Visual Studio Enterprise

![Скачивание редакций Visual Studio](VisualSutioInstall02.png){border-effect="line"}

Скачанный файл будет называться **VisualStudioSetup.exe** и весит он около **4Мб**. Вы сами понимаете что среда разработки
столько весить не может. Это просто установщик, который будет загружать все необходимые компоненты с серверов Микрософт. 
Из чего следует что для установки необходимо быть онлайн, то есть быть подключенным к интернету.

Ну в общем клацаем по файлу и начинаем установку.

В начале будет парочка таких окошек:

![Установка Visual Studio](VisualSutioInstall03.png){border-effect="line"}

![Установка Visual Studio](VisualSutioInstall04.png){border-effect="line"}

После этого вы увидите основное окно выбора компонентов установки:

На вкладке **Рабочие нагрузки** чекните указанные галки

![Установка Visual Studio](VisualSutioInstall05.png){border-effect="line" thumbnail="true" width="700"}

![Установка Visual Studio](VisualSutioInstall06.png){border-effect="line" thumbnail="true" width="700"}

Рабочие нагрузки, конечно заумное и не очень понятное название, но как есть. Короче это какие приложения вы сможете
делать с помощью Visual Studio. Полный дистрибутив студии занимает где-то 40Гб. И не всё это, и не всем разработчикам нужно.
Поэтому тут выбираем то что нам может пригодиться и даже с запасом.

Обратите внимание, что в правом нижнем углу выводится пространство необходимое для компонентов установки.

Ради спортивного интереса можете зайти на вкладку Отдельные компоненты и покрутить бегунок. Я часто шучу, что в пору
уже делать отдельный курс по установке Visual Studio. Это реально монстровый комбайн для производства софта на все
случаи жизни.

Все эти компоненты можно установить или удалить повторным запуском установщика. Поэтому не удаляйте файл установщика.

В принципе вы можете выбрать еще эти компоненты:

![Установка Visual Studio](VisualSutioInstall07.png){border-effect="line" thumbnail="true" width="700"}

В языковых пакетах выберите Английский и Русский языки.

![Установка Visual Studio](VisualSutioInstall08.png){border-effect="line" thumbnail="true" width="700"}

Хотя конечно же лучше стараться использовать английский интерфейс, так как большинство советов по Visual Studio 
используют именно английский интерфейс. Но по началу можно использовать и русский язык для интерфейса студии.

Расположение установки выберите исходя из своих предпочтений и дискового пространства. Я обычно всегда ставлю 
НЕ на диск С (не в раздел С, если быть более точным). Но сейчас, для простоты оставлю все по умолчанию.

![Установка Visual Studio](VisualSutioInstall09.png){border-effect="line" thumbnail="true" width="700"}

Жмем кнопку установить и ждем пока все закачается и установиться.

![Установка Visual Studio](VisualSutioInstall10.png){border-effect="line" thumbnail="true" width="700"}

После окончания установки необходимо перезагрузить компьютер.

![Установка Visual Studio](VisualSutioInstall11.png){border-effect="line" thumbnail="true" width="700"}

После перезагрузки в меню пуск появятся новые приложения.

![Установка Visual Studio](VisualSutioInstall12.png){border-effect="line"}

## Обновление Visual Studio {id="visual-studio_update"}
Пока писал эту статью вышло обновление студии, поэтому решил сразу же написать как обновлять Visual Studio.

Запускаем из меню пуск **Visual Studio Installer** и видим что-то вроде этого:

![Обновление Visual Studio](VisualStudioUpdate01.png){border-effect="line" thumbnail="true" width="700"}

Можете нажать **Посмотреть сведения** или же сразу же нажать **Обновить**, после чего начнётся обновление Visual Studio.

![Обновление Visual Studio](VisualStudioUpdate02.png){border-effect="line" thumbnail="true" width="700"}

После обновления закрываем окно установщика.

## Создание решения и консольного проекта в Visual Studio с операторами верхнего уровня
Запускаем Visual Studio. При первом запуске видим это окно:

![Создание проекта в Visual Studio](VisualStudioFirstProject01.png){border-effect="line" thumbnail="true" width="700"}

В Visual Studio, как и Visual Studio Code есть возможность создать учетную запись разработчика. Она позволяет делать
много полезных вещей, одна из которых синхронизация настроек студии между разными компьютерами, ну или быстрое 
восстановление настроек при переустановке студии. Мы пока этого касаться не будем. Поэтому жмем **Пропустить в этот раз**.

На следующем экране можно выбрать общую цветовую схему для всех или для определенного языка. Я оставлю как есть по
умолчанию. Эти настройки потом можно будет изменить.

![Создание проекта в Visual Studio](VisualStudioFirstProject02.png){border-effect="line" thumbnail="true" width="700"}

Ну и наконец запускаем Visual Studio. Первый запуск может занять какое-то время. Вы должны увидеть что-то вроде этого:

![Создание проекта в Visual Studio](VisualStudioFirstProject03.png){border-effect="line"}

Жмем **Создание проекта**. И выбираем все как показано на скриншоте.

1. Выбор языка
2. Выбор платформы
3. Выбор типа приложения
4. Выбор шаблона
5. Жмём далее

Обратите внимание, что выбранный шаблон предназначен для создания консольного приложения на C#, которое будет работать в
Windows, Linux и macOS.

Ниже есть шаблон для устаревшего .NET Framework и это приложение будет работать только в Windows.

![Создание проекта в Visual Studio](VisualStudioFirstProject05.png){border-effect="line"}

В следующем окне вводим все как на скриншоте. И обратите внимание по какому пути будет создан проект.

![Создание проекта в Visual Studio](VisualStudioFirstProject06.png){border-effect="line"}

На следующем экране ни какие галки не отмечаем, так как создаем проект с операторами верхнего уровня.
Платформа должна быть выбрана .NET 8.

![Создание проекта в Visual Studio](VisualStudioFirstProject07.png){border-effect="line"}

И жмем кнопку **Создать**. Создание проекта займет некоторое время.

![Создание проекта в Visual Studio](VisualStudioFirstProject08.png){border-effect="line"}

После создания проекта откроется среда Visual Studio.

![Создание проекта в Visual Studio](VisualStudioFirstProject09.png){border-effect="line" thumbnail="true" width="700"}

Измените код как нас скриншоте и запустите приложение нажав на кнопку запуска без отладки или комбинацию клавиш
`Ctrl+F5`.

![Запуск проекта в Visual Studio](VisualStudioFirstProject10.png){border-effect="line" thumbnail="true" width="700"}

Приложение запуститься в отдельном окне консоли.

![Запуск проекта в Visual Studio](VisualStudioFirstProject11.png){border-effect="line" thumbnail="true" width="700"}

Студия так же сообщила что наше приложение завершило работу с кодом 0, то есть все Ок.

Закройте окно консоли нажав любою клавишу или жмакнув по крестику на окне консоли.

Поздравляю! Вы создали и запустили первое приложение в Visual Studio.

У вас на текущий момент должна быть такая структура папок с проектами и решениями.

![Создание проекта в Visual Studio](VisualStudioFirstProject12.png){border-effect="line"  thumbnail="true" width="700"}

Обратите ещё раз внимание какая структура папок была создана для последнего решения и проекта.

## Добавление в решение консольного проекта в Visual Studio без операторов верхнего уровня {id="visual-studio_add_project"}
Нажмите правой кнопкой мышки на названии решения, и выберите **Добавить** и затем **Создать проект**.

![Добавление проекта в решение в Visual Studio](VisualStudioSecondProject01.png){border-effect="line" thumbnail="true" width="700"}

Откроется уже знакомое вам окно выбора параметров создаваемого приложения. Как правило, по умолчанию будет использован
последний тип проекта, который вы создавали. Выберите все как на скриншоте ниже и нажмите **Далее**

![Добавление проекта в решение в Visual Studio](VisualStudioSecondProject02.png){border-effect="line"}

В следующем окне задайте имя создаваемому проекту `ex0007_vs_project02` и нажмите **Далее**

![Добавление проекта в решение в Visual Studio](VisualStudioSecondProject03.png){border-effect="line"}

В следующем окне поставьте галку **Не использовать операторы верхнего уровня** и нажмите **Создать**

![Добавление проекта в решение в Visual Studio](VisualStudioSecondProject04.png){border-effect="line"}

Вы должны увидеть что-то вроде этого:

![Добавление проекта в решение в Visual Studio](VisualStudioSecondProject05.png){border-effect="line" thumbnail="true" width="700"}

