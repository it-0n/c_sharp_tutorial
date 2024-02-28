# Установка .NET SDK 8 в WSL
[WSL](https://learn.microsoft.com/ru-ru/windows/wsl/) или [Windows Subsystem for Linux](https://learn.microsoft.com/ru-ru/windows/wsl/faq) -
это функция операционной системы Windows, которая позволяет запускать файловую
систему Linux, а также программы командной строки Linux и приложения графического пользовательского интерфейса
непосредственно в Windows, наряду с традиционными классическими приложениями и приложениями Windows.

Простыми словами это возможность запустить полноценный Linux внутри Windows. То есть вы можете работать одновременно и в Windows,
и в Linux на вашем компьютере. Здорово же?

Чтобы воспользоваться [WSL в Windows его сперва надо установить](https://learn.microsoft.com/ru-ru/windows/wsl/install).

## Установка WSL
Установка WSL очень простая. В командной строке запущенной с правами Администратора надо дать команду:

`wsl --install`

Эта команда включит функции, необходимые для запуска WSL и установит Ubuntu. **После окончания работы
этой команды перезагрузите компьютер.**

Скриншоты работы команды:

![WSL install on Windows](wsl_install01.png){border-effect="line"}

![WSL install on Windows](wsl_install02.png){border-effect="line"}

![WSL install on Windows](wsl_install03.png){border-effect="line"}

Всё очень просто! Неправда ли? 